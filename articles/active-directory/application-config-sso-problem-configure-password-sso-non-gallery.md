---
title: Problem configuring password single sign-on for a non-gallery application | Microsoft Docs
description: Understand the common problems people face when configuring Password Single Sign-on for custom non-gallery applications that are not listed in the Azure AD Application Gallery
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
ms.openlocfilehash: e2ee7460aa1204c6470f1ec481ecb01a00858cce
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564316"
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="4c967-103">Problem configuring password single sign-on for a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="4c967-103">Problem configuring password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="4c967-104">This article help you to understand the common problems people face when configuring **Password single sign-on** with a non-gallery application.</span><span class="sxs-lookup"><span data-stu-id="4c967-104">This article help you to understand the common problems people face when configuring **Password single sign-on** with a non-gallery application.</span></span>

## <a name="how-to-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="4c967-105">How to capture sign-in fields for an application</span><span class="sxs-lookup"><span data-stu-id="4c967-105">How to capture sign-in fields for an application</span></span>

<span data-ttu-id="4c967-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span><span class="sxs-lookup"><span data-stu-id="4c967-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span></span>

<span data-ttu-id="4c967-107">There are two ways you can capture sign-in fields for your custom applications:</span><span class="sxs-lookup"><span data-stu-id="4c967-107">There are two ways you can capture sign-in fields for your custom applications:</span></span>

-   <span data-ttu-id="4c967-108">Automatic sign-in field capture</span><span class="sxs-lookup"><span data-stu-id="4c967-108">Automatic sign-in field capture</span></span>

-   <span data-ttu-id="4c967-109">Manual sign-in field capture</span><span class="sxs-lookup"><span data-stu-id="4c967-109">Manual sign-in field capture</span></span>

<span data-ttu-id="4c967-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for the username and password input** field.</span><span class="sxs-lookup"><span data-stu-id="4c967-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for the username and password input** field.</span></span> <span data-ttu-id="4c967-111">The way this works is by scraping the HTML on the page to find DIV IDs that match certain criteria and by then saving that metadata for this application so we can replay passwords to it later.</span><span class="sxs-lookup"><span data-stu-id="4c967-111">The way this works is by scraping the HTML on the page to find DIV IDs that match certain criteria and by then saving that metadata for this application so we can replay passwords to it later.</span></span>

<span data-ttu-id="4c967-112">**Manual sign-in field capture** can be used in the case that the application **vendor does not label** the input fields used for sign in.</span><span class="sxs-lookup"><span data-stu-id="4c967-112">**Manual sign-in field capture** can be used in the case that the application **vendor does not label** the input fields used for sign in.</span></span> <span data-ttu-id="4c967-113">Manual sign-in field capture can also be used in the case when the **vendor renders multiple fields** which cannot be auto-detected.</span><span class="sxs-lookup"><span data-stu-id="4c967-113">Manual sign-in field capture can also be used in the case when the **vendor renders multiple fields** which cannot be auto-detected.</span></span> <span data-ttu-id="4c967-114">Azure AD can store data for as many fields as are on the sign in page, so long as you tell us where those fields are on the page.</span><span class="sxs-lookup"><span data-stu-id="4c967-114">Azure AD can store data for as many fields as are on the sign in page, so long as you tell us where those fields are on the page.</span></span>

<span data-ttu-id="4c967-115">In general, **if automatic sign-in field capture does not work, we always suggest trying the manual option.**</span><span class="sxs-lookup"><span data-stu-id="4c967-115">In general, **if automatic sign-in field capture does not work, we always suggest trying the manual option.**</span></span>

### <a name="how-to-automatically-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="4c967-116">How to automatically capture sign-in fields for an application</span><span class="sxs-lookup"><span data-stu-id="4c967-116">How to automatically capture sign-in fields for an application</span></span>

<span data-ttu-id="4c967-117">To configure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="4c967-117">To configure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow the steps below:</span></span>

1.  <span data-ttu-id="4c967-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="4c967-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4c967-119">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4c967-119">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4c967-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="4c967-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4c967-121">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4c967-121">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4c967-122">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="4c967-122">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="4c967-123">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="4c967-123">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4c967-124">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4c967-124">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="4c967-125">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4c967-125">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4c967-126">Select the mode **Password-based Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="4c967-126">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="4c967-127">Enter the **Sign-on URL**.</span><span class="sxs-lookup"><span data-stu-id="4c967-127">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="4c967-128">This is the URL where users enter their username and password to sign in to.</span><span class="sxs-lookup"><span data-stu-id="4c967-128">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="4c967-129">**Ensure the sign in fields are visible at the URL you provide**.</span><span class="sxs-lookup"><span data-stu-id="4c967-129">**Ensure the sign in fields are visible at the URL you provide**.</span></span>

10. <span data-ttu-id="4c967-130">Click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4c967-130">Click the **Save** button.</span></span>

11. <span data-ttu-id="4c967-131">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span><span class="sxs-lookup"><span data-stu-id="4c967-131">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span>

## <a name="how-to-manually-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="4c967-132">How to manually capture sign-in fields for an application</span><span class="sxs-lookup"><span data-stu-id="4c967-132">How to manually capture sign-in fields for an application</span></span>

<span data-ttu-id="4c967-133">To manually capture sign in fields, you must first have the Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span><span class="sxs-lookup"><span data-stu-id="4c967-133">To manually capture sign in fields, you must first have the Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span></span> <span data-ttu-id="4c967-134">To install the browser extension, follow the steps in the [How to install the Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span><span class="sxs-lookup"><span data-stu-id="4c967-134">To install the browser extension, follow the steps in the [How to install the Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span></span>

<span data-ttu-id="4c967-135">To configure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="4c967-135">To configure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow the steps below:</span></span>

1.  <span data-ttu-id="4c967-136">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="4c967-136">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="4c967-137">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4c967-137">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="4c967-138">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="4c967-138">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="4c967-139">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4c967-139">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="4c967-140">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="4c967-140">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="4c967-141">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="4c967-141">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="4c967-142">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4c967-142">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="4c967-143">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="4c967-143">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="4c967-144">Select the mode **Password-based Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="4c967-144">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="4c967-145">Enter the **Sign-on URL**.</span><span class="sxs-lookup"><span data-stu-id="4c967-145">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="4c967-146">This is the URL where users enter their username and password to sign in to.</span><span class="sxs-lookup"><span data-stu-id="4c967-146">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="4c967-147">**Ensure the sign in fields are visible at the URL you provide**.</span><span class="sxs-lookup"><span data-stu-id="4c967-147">**Ensure the sign in fields are visible at the URL you provide**.</span></span>

10. <span data-ttu-id="4c967-148">Click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4c967-148">Click the **Save** button.</span></span>

11. <span data-ttu-id="4c967-149">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span><span class="sxs-lookup"><span data-stu-id="4c967-149">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span> <span data-ttu-id="4c967-150">In the case that this fails, you can **change the sign-in mode to use manual sign-in field capture** by continuing to step 12.</span><span class="sxs-lookup"><span data-stu-id="4c967-150">In the case that this fails, you can **change the sign-in mode to use manual sign-in field capture** by continuing to step 12.</span></span>

12. <span data-ttu-id="4c967-151">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span><span class="sxs-lookup"><span data-stu-id="4c967-151">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span></span>

13. <span data-ttu-id="4c967-152">Select the **Manually detect sign-in fields** configuration option.</span><span class="sxs-lookup"><span data-stu-id="4c967-152">Select the **Manually detect sign-in fields** configuration option.</span></span>

14. <span data-ttu-id="4c967-153">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="4c967-153">Click **Ok**.</span></span>

15. <span data-ttu-id="4c967-154">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4c967-154">Click **Save**.</span></span>

16. <span data-ttu-id="4c967-155">Follow the on screen instructions to use the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4c967-155">Follow the on screen instructions to use the Access Panel.</span></span>

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a><span data-ttu-id="4c967-156">I see a “We couldn’t find any sign-in fields at that URL” error</span><span class="sxs-lookup"><span data-stu-id="4c967-156">I see a “We couldn’t find any sign-in fields at that URL” error</span></span>

<span data-ttu-id="4c967-157">You see this error when automatic detection of sign-in fields fails.</span><span class="sxs-lookup"><span data-stu-id="4c967-157">You see this error when automatic detection of sign-in fields fails.</span></span> <span data-ttu-id="4c967-158">To resolve this issue, try manual sign-in field detection by following the steps in the [How to manually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span><span class="sxs-lookup"><span data-stu-id="4c967-158">To resolve this issue, try manual sign-in field detection by following the steps in the [How to manually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span></span>

## <a name="i-see-an-unable-to-save-single-sign-on-configuration-error"></a><span data-ttu-id="4c967-159">I see an “Unable to save Single Sign-on configuration” error</span><span class="sxs-lookup"><span data-stu-id="4c967-159">I see an “Unable to save Single Sign-on configuration” error</span></span>

<span data-ttu-id="4c967-160">In certain rare cases, updating the single sign-on configuration can fail.</span><span class="sxs-lookup"><span data-stu-id="4c967-160">In certain rare cases, updating the single sign-on configuration can fail.</span></span> <span data-ttu-id="4c967-161">TO resolve this try saving the single sign-on configuration again.</span><span class="sxs-lookup"><span data-stu-id="4c967-161">TO resolve this try saving the single sign-on configuration again.</span></span>

<span data-ttu-id="4c967-162">If this continues to fail consistently, open a support case and provide the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span><span class="sxs-lookup"><span data-stu-id="4c967-162">If this continues to fail consistently, open a support case and provide the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span></span>

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a><span data-ttu-id="4c967-163">I cannot manually detect sign in fields for my application</span><span class="sxs-lookup"><span data-stu-id="4c967-163">I cannot manually detect sign in fields for my application</span></span>

<span data-ttu-id="4c967-164">Some of the behaviors you might see when manual detection is not working include:</span><span class="sxs-lookup"><span data-stu-id="4c967-164">Some of the behaviors you might see when manual detection is not working include:</span></span>

-   <span data-ttu-id="4c967-165">The manual capture process appeared to work, but the fields captured were not correct</span><span class="sxs-lookup"><span data-stu-id="4c967-165">The manual capture process appeared to work, but the fields captured were not correct</span></span>

-   <span data-ttu-id="4c967-166">The right fields don’t get highlighted when performing the capture process</span><span class="sxs-lookup"><span data-stu-id="4c967-166">The right fields don’t get highlighted when performing the capture process</span></span>

-   <span data-ttu-id="4c967-167">The capture process takes me to the application’s login page as expected, but nothing happens</span><span class="sxs-lookup"><span data-stu-id="4c967-167">The capture process takes me to the application’s login page as expected, but nothing happens</span></span>

-   <span data-ttu-id="4c967-168">Manual capture appears to work, but SSO doesn’t happen when my users navigate to the application from the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4c967-168">Manual capture appears to work, but SSO doesn’t happen when my users navigate to the application from the Access Panel.</span></span>

<span data-ttu-id="4c967-169">check the following if you encounter any of these issues:</span><span class="sxs-lookup"><span data-stu-id="4c967-169">check the following if you encounter any of these issues:</span></span>

-   <span data-ttu-id="4c967-170">Ensure that you have the latest version of the access panel browser extension **installed** and **enabled** by following the steps in the [How to install the Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span><span class="sxs-lookup"><span data-stu-id="4c967-170">Ensure that you have the latest version of the access panel browser extension **installed** and **enabled** by following the steps in the [How to install the Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="4c967-171">Ensure that you are not attempting the capture process while your browser in **incognito, inPrivate, or Private mode**.</span><span class="sxs-lookup"><span data-stu-id="4c967-171">Ensure that you are not attempting the capture process while your browser in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="4c967-172">The access panel extension is not supported in these modes.</span><span class="sxs-lookup"><span data-stu-id="4c967-172">The access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="4c967-173">Ensure that your users are not trying to sign in to the application from the access panel while in **incognito, inPrivate, or Private mode**.</span><span class="sxs-lookup"><span data-stu-id="4c967-173">Ensure that your users are not trying to sign in to the application from the access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="4c967-174">The access panel extension is not supported in these modes.</span><span class="sxs-lookup"><span data-stu-id="4c967-174">The access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="4c967-175">Try the manual capture process again, ensuring the red markers are over the correct fields.</span><span class="sxs-lookup"><span data-stu-id="4c967-175">Try the manual capture process again, ensuring the red markers are over the correct fields.</span></span>

-   <span data-ttu-id="4c967-176">If the manual capture process seems to hang, or the sign in page doesn’t do anything (case 3 above), try the manual capture process again.</span><span class="sxs-lookup"><span data-stu-id="4c967-176">If the manual capture process seems to hang, or the sign in page doesn’t do anything (case 3 above), try the manual capture process again.</span></span> <span data-ttu-id="4c967-177">But, this time after completing the process, press the **F12** button to open your browser’s developer console.</span><span class="sxs-lookup"><span data-stu-id="4c967-177">But, this time after completing the process, press the **F12** button to open your browser’s developer console.</span></span> <span data-ttu-id="4c967-178">Once there, open the **console** and type **window.location=”&lt;enter the sign in url you specified when configuring the app&gt;”** and then press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="4c967-178">Once there, open the **console** and type **window.location=”&lt;enter the sign in url you specified when configuring the app&gt;”** and then press **Enter**.</span></span> <span data-ttu-id="4c967-179">This force a page redirect which end the capture process and store the fields that have been captured.</span><span class="sxs-lookup"><span data-stu-id="4c967-179">This force a page redirect which end the capture process and store the fields that have been captured.</span></span>

<span data-ttu-id="4c967-180">If none of these approaches work for you, we can help.</span><span class="sxs-lookup"><span data-stu-id="4c967-180">If none of these approaches work for you, we can help.</span></span> <span data-ttu-id="4c967-181">Open a support case with the details of what you tried, as well as the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span><span class="sxs-lookup"><span data-stu-id="4c967-181">Open a support case with the details of what you tried, as well as the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="4c967-182">How to install the Access Panel Browser extension</span><span class="sxs-lookup"><span data-stu-id="4c967-182">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="4c967-183">To install the Access Panel Browser extension, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="4c967-183">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="4c967-184">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c967-184">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="4c967-185">click a **password-SSO application** in the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="4c967-185">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="4c967-186">In the prompt asking to install the software, select **Install Now**.</span><span class="sxs-lookup"><span data-stu-id="4c967-186">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="4c967-187">Based on your browser you be directed to the download link.</span><span class="sxs-lookup"><span data-stu-id="4c967-187">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="4c967-188">**Add** the extension to your browser.</span><span class="sxs-lookup"><span data-stu-id="4c967-188">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="4c967-189">If your browser asks, select to either **Enable** or **Allow** the extension.</span><span class="sxs-lookup"><span data-stu-id="4c967-189">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="4c967-190">Once installed, **restart** your browser session.</span><span class="sxs-lookup"><span data-stu-id="4c967-190">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="4c967-191">Sign in into the Access Panel and see if you can **launch** your password-SSO applications.</span><span class="sxs-lookup"><span data-stu-id="4c967-191">Sign in into the Access Panel and see if you can **launch** your password-SSO applications.</span></span>

<span data-ttu-id="4c967-192">You may also download the extension for Chrome and Firefox from the direct links below:</span><span class="sxs-lookup"><span data-stu-id="4c967-192">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="4c967-193">Chrome Access Panel Extension</span><span class="sxs-lookup"><span data-stu-id="4c967-193">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="4c967-194">Firefox Access Panel Extension</span><span class="sxs-lookup"><span data-stu-id="4c967-194">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-to-see-the-details-of-a-portal-notification"></a><span data-ttu-id="4c967-195">How to see the details of a portal notification</span><span class="sxs-lookup"><span data-stu-id="4c967-195">How to see the details of a portal notification</span></span>

<span data-ttu-id="4c967-196">You can see the details of any portal notification by following the steps below:</span><span class="sxs-lookup"><span data-stu-id="4c967-196">You can see the details of any portal notification by following the steps below:</span></span>

1.  <span data-ttu-id="4c967-197">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4c967-197">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span></span>

2.  <span data-ttu-id="4c967-198">Select any notification in an **Error** state (those with a red (!) next to them).</span><span class="sxs-lookup"><span data-stu-id="4c967-198">Select any notification in an **Error** state (those with a red (!) next to them).</span></span>

  ><span data-ttu-id="4c967-199">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span><span class="sxs-lookup"><span data-stu-id="4c967-199">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
  >
  >

3.  <span data-ttu-id="4c967-200">This open the **Notification Details** blade.</span><span class="sxs-lookup"><span data-stu-id="4c967-200">This open the **Notification Details** blade.</span></span>

4.  <span data-ttu-id="4c967-201">Use this information yourself to understand more details about the problem.</span><span class="sxs-lookup"><span data-stu-id="4c967-201">Use this information yourself to understand more details about the problem.</span></span>

5.  <span data-ttu-id="4c967-202">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span><span class="sxs-lookup"><span data-stu-id="4c967-202">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span></span>

6.  <span data-ttu-id="4c967-203">Click the **copy** **icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer.</span><span class="sxs-lookup"><span data-stu-id="4c967-203">Click the **copy** **icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer.</span></span>

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a><span data-ttu-id="4c967-204">How to get help by sending notification details to a support engineer</span><span class="sxs-lookup"><span data-stu-id="4c967-204">How to get help by sending notification details to a support engineer</span></span>

<span data-ttu-id="4c967-205">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span><span class="sxs-lookup"><span data-stu-id="4c967-205">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="4c967-206">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span><span class="sxs-lookup"><span data-stu-id="4c967-206">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="4c967-207">Notification Details Explained</span><span class="sxs-lookup"><span data-stu-id="4c967-207">Notification Details Explained</span></span>

<span data-ttu-id="4c967-208">The below explains more what each of the notification items means, and gives examples of each of them.</span><span class="sxs-lookup"><span data-stu-id="4c967-208">The below explains more what each of the notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="4c967-209">Essential Notification Items</span><span class="sxs-lookup"><span data-stu-id="4c967-209">Essential Notification Items</span></span>

-   <span data-ttu-id="4c967-210">**Title** – the descriptive title of the notification</span><span class="sxs-lookup"><span data-stu-id="4c967-210">**Title** – the descriptive title of the notification</span></span>

    -   <span data-ttu-id="4c967-211">Example – **Application proxy settings**</span><span class="sxs-lookup"><span data-stu-id="4c967-211">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="4c967-212">**Description** – the description of what occurred as a result of the operation</span><span class="sxs-lookup"><span data-stu-id="4c967-212">**Description** – the description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="4c967-213">Example – **Internal url entered is already being used by another application**</span><span class="sxs-lookup"><span data-stu-id="4c967-213">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="4c967-214">**Notification Id** – the unique id of the notification</span><span class="sxs-lookup"><span data-stu-id="4c967-214">**Notification Id** – the unique id of the notification</span></span>

    -   <span data-ttu-id="4c967-215">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="4c967-215">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="4c967-216">**Client Request Id** – the specific request id made by your browser</span><span class="sxs-lookup"><span data-stu-id="4c967-216">**Client Request Id** – the specific request id made by your browser</span></span>

    -   <span data-ttu-id="4c967-217">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="4c967-217">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="4c967-218">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span><span class="sxs-lookup"><span data-stu-id="4c967-218">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span></span>

    -   <span data-ttu-id="4c967-219">Example – **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="4c967-219">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="4c967-220">**Internal Transaction Id** – the internal ID we can use to look the error up in our systems</span><span class="sxs-lookup"><span data-stu-id="4c967-220">**Internal Transaction Id** – the internal ID we can use to look the error up in our systems</span></span>

    -   <span data-ttu-id="4c967-221">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="4c967-221">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="4c967-222">**UPN** – the user who performed the operation</span><span class="sxs-lookup"><span data-stu-id="4c967-222">**UPN** – the user who performed the operation</span></span>

    -   <span data-ttu-id="4c967-223">Example – **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="4c967-223">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="4c967-224">**Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of</span><span class="sxs-lookup"><span data-stu-id="4c967-224">**Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of</span></span>

    -   <span data-ttu-id="4c967-225">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="4c967-225">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="4c967-226">**User object Id** – the unique ID of the user who performed the operation</span><span class="sxs-lookup"><span data-stu-id="4c967-226">**User object Id** – the unique ID of the user who performed the operation</span></span>

    -   <span data-ttu-id="4c967-227">Example – **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="4c967-227">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="4c967-228">Detailed Notification Items</span><span class="sxs-lookup"><span data-stu-id="4c967-228">Detailed Notification Items</span></span>

-   <span data-ttu-id="4c967-229">**Display Name** – **(can be empty)** a more detailed display name for the error</span><span class="sxs-lookup"><span data-stu-id="4c967-229">**Display Name** – **(can be empty)** a more detailed display name for the error</span></span>

    -   <span data-ttu-id="4c967-230">Example \*– **Application proxy settings**</span><span class="sxs-lookup"><span data-stu-id="4c967-230">Example \*– **Application proxy settings**</span></span>

-   <span data-ttu-id="4c967-231">**Status** – the specific status of the notification</span><span class="sxs-lookup"><span data-stu-id="4c967-231">**Status** – the specific status of the notification</span></span>

    -   <span data-ttu-id="4c967-232">Example \*– **Failed**</span><span class="sxs-lookup"><span data-stu-id="4c967-232">Example \*– **Failed**</span></span>

-   <span data-ttu-id="4c967-233">**Object Id** – **(can be empty)** the object ID against which the operation was performed</span><span class="sxs-lookup"><span data-stu-id="4c967-233">**Object Id** – **(can be empty)** the object ID against which the operation was performed</span></span>

    -   <span data-ttu-id="4c967-234">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="4c967-234">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="4c967-235">**Details** – the detailed description of what occurred as a result of the operation</span><span class="sxs-lookup"><span data-stu-id="4c967-235">**Details** – the detailed description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="4c967-236">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span><span class="sxs-lookup"><span data-stu-id="4c967-236">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="4c967-237">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span><span class="sxs-lookup"><span data-stu-id="4c967-237">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

    -   <span data-ttu-id="4c967-238">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="4c967-238">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c967-239">Next steps</span><span class="sxs-lookup"><span data-stu-id="4c967-239">Next steps</span></span>
[<span data-ttu-id="4c967-240">Provide single sign-on to your apps with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="4c967-240">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

