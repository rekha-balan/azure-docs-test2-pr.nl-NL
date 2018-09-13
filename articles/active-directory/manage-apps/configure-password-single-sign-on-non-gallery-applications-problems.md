---
title: Problem configuring password single sign-on for a non-gallery application | Microsoft Docs
description: Understand the common problems people face when configuring Password Single Sign-on for custom non-gallery applications that are not listed in the Azure AD Application Gallery
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
ms.openlocfilehash: 3675889e583fbe2bf949891c3d6b4d5f731e6ac1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868061"
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="c3bb5-103">Problem configuring password single sign-on for a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="c3bb5-103">Problem configuring password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="c3bb5-104">This article help you to understand the common problems people face when configuring **Password single sign-on** with a non-gallery application.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-104">This article help you to understand the common problems people face when configuring **Password single sign-on** with a non-gallery application.</span></span>

## <a name="how-to-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="c3bb5-105">How to capture sign-in fields for an application</span><span class="sxs-lookup"><span data-stu-id="c3bb5-105">How to capture sign-in fields for an application</span></span>

<span data-ttu-id="c3bb5-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span></span>

<span data-ttu-id="c3bb5-107">There are two ways you can capture sign-in fields for your custom applications:</span><span class="sxs-lookup"><span data-stu-id="c3bb5-107">There are two ways you can capture sign-in fields for your custom applications:</span></span>

-   <span data-ttu-id="c3bb5-108">Automatic sign-in field capture</span><span class="sxs-lookup"><span data-stu-id="c3bb5-108">Automatic sign-in field capture</span></span>

-   <span data-ttu-id="c3bb5-109">Manual sign-in field capture</span><span class="sxs-lookup"><span data-stu-id="c3bb5-109">Manual sign-in field capture</span></span>

<span data-ttu-id="c3bb5-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for the username and password input** field.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for the username and password input** field.</span></span> <span data-ttu-id="c3bb5-111">The way this works is by scraping the HTML on the page to find DIV IDs that match certain criteria and by then saving that metadata for this application to replay passwords to it later.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-111">The way this works is by scraping the HTML on the page to find DIV IDs that match certain criteria and by then saving that metadata for this application to replay passwords to it later.</span></span>

<span data-ttu-id="c3bb5-112">**Manual sign-in field capture** can be used in the case that the application **vendor does not label** the input fields used for sign-in.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-112">**Manual sign-in field capture** can be used in the case that the application **vendor does not label** the input fields used for sign-in.</span></span> <span data-ttu-id="c3bb5-113">Manual sign-in field capture can also be used in the case when the **vendor renders multiple fields** that cannot be auto-detected.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-113">Manual sign-in field capture can also be used in the case when the **vendor renders multiple fields** that cannot be auto-detected.</span></span> <span data-ttu-id="c3bb5-114">Azure AD can store data for as many fields as are on the sign-in page, so long as you tell us where those fields are on the page.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-114">Azure AD can store data for as many fields as are on the sign-in page, so long as you tell us where those fields are on the page.</span></span>

<span data-ttu-id="c3bb5-115">In general, **if automatic sign-in field capture does not work, try the manual option.**</span><span class="sxs-lookup"><span data-stu-id="c3bb5-115">In general, **if automatic sign-in field capture does not work, try the manual option.**</span></span>

### <a name="how-to-automatically-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="c3bb5-116">How to automatically capture sign-in fields for an application</span><span class="sxs-lookup"><span data-stu-id="c3bb5-116">How to automatically capture sign-in fields for an application</span></span>

<span data-ttu-id="c3bb5-117">To configure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="c3bb5-117">To configure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow the steps below:</span></span>

1.  <span data-ttu-id="c3bb5-118">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="c3bb5-118">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c3bb5-119">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-119">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="c3bb5-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c3bb5-121">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-121">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="c3bb5-122">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-122">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="c3bb5-123">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="c3bb5-123">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="c3bb5-124">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-124">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="c3bb5-125">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-125">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="c3bb5-126">Select the mode **Password-based Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="c3bb5-126">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="c3bb5-127">Enter the **Sign-on URL**, the URL where users enter their username and password to sign in.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-127">Enter the **Sign-on URL**, the URL where users enter their username and password to sign in.</span></span> <span data-ttu-id="c3bb5-128">**Ensure the sign-in fields are visible at the URL you provide**.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-128">**Ensure the sign-in fields are visible at the URL you provide**.</span></span>

10. <span data-ttu-id="c3bb5-129">Click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-129">Click the **Save** button.</span></span>

11. <span data-ttu-id="c3bb5-130">Once you do that, that URL is automatically scraped for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-130">Once you do that, that URL is automatically scraped for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span>

## <a name="how-to-manually-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="c3bb5-131">How to manually capture sign-in fields for an application</span><span class="sxs-lookup"><span data-stu-id="c3bb5-131">How to manually capture sign-in fields for an application</span></span>

<span data-ttu-id="c3bb5-132">To manually capture sign-in fields, you must first have the Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span><span class="sxs-lookup"><span data-stu-id="c3bb5-132">To manually capture sign-in fields, you must first have the Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span></span> <span data-ttu-id="c3bb5-133">To install the browser extension, follow the steps in the [How to install the Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-133">To install the browser extension, follow the steps in the [How to install the Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span></span>

<span data-ttu-id="c3bb5-134">To configure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="c3bb5-134">To configure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow the steps below:</span></span>

1.  <span data-ttu-id="c3bb5-135">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="c3bb5-135">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c3bb5-136">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-136">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="c3bb5-137">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-137">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c3bb5-138">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-138">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="c3bb5-139">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-139">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="c3bb5-140">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="c3bb5-140">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="c3bb5-141">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-141">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="c3bb5-142">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-142">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="c3bb5-143">Select the mode **Password-based Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="c3bb5-143">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="c3bb5-144">Enter the **Sign-on URL**, the URL where users enter their username and password to sign in.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-144">Enter the **Sign-on URL**, the URL where users enter their username and password to sign in.</span></span> <span data-ttu-id="c3bb5-145">**Ensure the sign-in fields are visible at the URL you provide**.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-145">**Ensure the sign-in fields are visible at the URL you provide**.</span></span>

10. <span data-ttu-id="c3bb5-146">Click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-146">Click the **Save** button.</span></span>

11. <span data-ttu-id="c3bb5-147">Once you do that, that URL is automatically scraped for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-147">Once you do that, that URL is automatically scraped for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span> <span data-ttu-id="c3bb5-148">In the case of failure, you can **change the sign-in mode to use manual sign-in field capture** by continuing to step 12.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-148">In the case of failure, you can **change the sign-in mode to use manual sign-in field capture** by continuing to step 12.</span></span>

12. <span data-ttu-id="c3bb5-149">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-149">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span></span>

13. <span data-ttu-id="c3bb5-150">Select the **Manually detect sign-in fields** configuration option.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-150">Select the **Manually detect sign-in fields** configuration option.</span></span>

14. <span data-ttu-id="c3bb5-151">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-151">Click **Ok**.</span></span>

15. <span data-ttu-id="c3bb5-152">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-152">Click **Save**.</span></span>

16. <span data-ttu-id="c3bb5-153">Follow the on screen instructions to use the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-153">Follow the on screen instructions to use the Access Panel.</span></span>

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a><span data-ttu-id="c3bb5-154">I see a “We couldn’t find any sign-in fields at that URL” error</span><span class="sxs-lookup"><span data-stu-id="c3bb5-154">I see a “We couldn’t find any sign-in fields at that URL” error</span></span>

<span data-ttu-id="c3bb5-155">You see this error when automatic detection of sign-in fields fails.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-155">You see this error when automatic detection of sign-in fields fails.</span></span> <span data-ttu-id="c3bb5-156">To resolve the issue, try manual sign-in field detection by following the steps in the [How to manually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-156">To resolve the issue, try manual sign-in field detection by following the steps in the [How to manually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span></span>

## <a name="i-see-an-unable-to-save-single-sign-on-configuration-error"></a><span data-ttu-id="c3bb5-157">I see an “Unable to save Single Sign-on configuration” error</span><span class="sxs-lookup"><span data-stu-id="c3bb5-157">I see an “Unable to save Single Sign-on configuration” error</span></span>

<span data-ttu-id="c3bb5-158">In certain rare cases, updating the single sign-on configuration can fail.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-158">In certain rare cases, updating the single sign-on configuration can fail.</span></span> <span data-ttu-id="c3bb5-159">To resolve, try saving the single sign-on configuration again.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-159">To resolve, try saving the single sign-on configuration again.</span></span>

<span data-ttu-id="c3bb5-160">If it continues to fail consistently, open a support case and provide the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-160">If it continues to fail consistently, open a support case and provide the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span></span>

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a><span data-ttu-id="c3bb5-161">I cannot manually detect sign-in fields for my application</span><span class="sxs-lookup"><span data-stu-id="c3bb5-161">I cannot manually detect sign-in fields for my application</span></span>

<span data-ttu-id="c3bb5-162">Some of the behaviors you might see when manual detection is not working include:</span><span class="sxs-lookup"><span data-stu-id="c3bb5-162">Some of the behaviors you might see when manual detection is not working include:</span></span>

-   <span data-ttu-id="c3bb5-163">The manual capture process appeared to work, but the fields captured were not correct</span><span class="sxs-lookup"><span data-stu-id="c3bb5-163">The manual capture process appeared to work, but the fields captured were not correct</span></span>

-   <span data-ttu-id="c3bb5-164">The right fields don’t get highlighted when performing the capture process</span><span class="sxs-lookup"><span data-stu-id="c3bb5-164">The right fields don’t get highlighted when performing the capture process</span></span>

-   <span data-ttu-id="c3bb5-165">The capture process takes me to the application’s login page as expected, but nothing happens</span><span class="sxs-lookup"><span data-stu-id="c3bb5-165">The capture process takes me to the application’s login page as expected, but nothing happens</span></span>

-   <span data-ttu-id="c3bb5-166">Manual capture appears to work, but SSO doesn’t happen when my users navigate to the application from the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-166">Manual capture appears to work, but SSO doesn’t happen when my users navigate to the application from the Access Panel.</span></span>

<span data-ttu-id="c3bb5-167">check the following if you encounter any of these issues:</span><span class="sxs-lookup"><span data-stu-id="c3bb5-167">check the following if you encounter any of these issues:</span></span>

-   <span data-ttu-id="c3bb5-168">Ensure that you have the latest version of the access panel browser extension **installed** and **enabled** by following the steps in the [How to install the Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-168">Ensure that you have the latest version of the access panel browser extension **installed** and **enabled** by following the steps in the [How to install the Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="c3bb5-169">Ensure that you are not attempting the capture process while your browser in **incognito, inPrivate, or Private mode**.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-169">Ensure that you are not attempting the capture process while your browser in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="c3bb5-170">The access panel extension is not supported in these modes.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-170">The access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="c3bb5-171">Ensure that your users are not trying to sign in to the application from the access panel while in **incognito, inPrivate, or Private mode**.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-171">Ensure that your users are not trying to sign in to the application from the access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="c3bb5-172">The access panel extension is not supported in these modes.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-172">The access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="c3bb5-173">Try the manual capture process again, ensuring the red markers are over the correct fields.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-173">Try the manual capture process again, ensuring the red markers are over the correct fields.</span></span>

-   <span data-ttu-id="c3bb5-174">If the manual capture process seems to hang, or the sign-in page doesn’t do anything (case 3 above), try the manual capture process again.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-174">If the manual capture process seems to hang, or the sign-in page doesn’t do anything (case 3 above), try the manual capture process again.</span></span> <span data-ttu-id="c3bb5-175">But, this time after completing the process, press the **F12** button to open your browser’s developer console.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-175">But, this time after completing the process, press the **F12** button to open your browser’s developer console.</span></span> <span data-ttu-id="c3bb5-176">Once there, open the **console** and type **window.location=”&lt;enter the sign-in url you specified when configuring the app&gt;”** and then press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-176">Once there, open the **console** and type **window.location=”&lt;enter the sign-in url you specified when configuring the app&gt;”** and then press **Enter**.</span></span> <span data-ttu-id="c3bb5-177">This forces a page redirect that ends the capture process and stores the fields that have been captured.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-177">This forces a page redirect that ends the capture process and stores the fields that have been captured.</span></span>

<span data-ttu-id="c3bb5-178">If none of these approaches work for you, support can help.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-178">If none of these approaches work for you, support can help.</span></span> <span data-ttu-id="c3bb5-179">Open a support case with the details of what you tried, as well as the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span><span class="sxs-lookup"><span data-stu-id="c3bb5-179">Open a support case with the details of what you tried, as well as the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="c3bb5-180">How to install the Access Panel Browser extension</span><span class="sxs-lookup"><span data-stu-id="c3bb5-180">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="c3bb5-181">To install the Access Panel Browser extension, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="c3bb5-181">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="c3bb5-182">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-182">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="c3bb5-183">click a **password-SSO application** in the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-183">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="c3bb5-184">In the prompt asking to install the software, select **Install Now**.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-184">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="c3bb5-185">Based on your browser you be directed to the download link.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-185">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="c3bb5-186">**Add** the extension to your browser.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-186">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="c3bb5-187">If your browser asks, select to either **Enable** or **Allow** the extension.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-187">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="c3bb5-188">Once installed, **restart** your browser session.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-188">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="c3bb5-189">Sign in into the Access Panel and see if you can **launch** your password-SSO applications.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-189">Sign in into the Access Panel and see if you can **launch** your password-SSO applications.</span></span>

<span data-ttu-id="c3bb5-190">You may also download the extension for Chrome and Firefox from the direct links below:</span><span class="sxs-lookup"><span data-stu-id="c3bb5-190">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="c3bb5-191">Chrome Access Panel Extension</span><span class="sxs-lookup"><span data-stu-id="c3bb5-191">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="c3bb5-192">Firefox Access Panel Extension</span><span class="sxs-lookup"><span data-stu-id="c3bb5-192">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-to-see-the-details-of-a-portal-notification"></a><span data-ttu-id="c3bb5-193">How to see the details of a portal notification</span><span class="sxs-lookup"><span data-stu-id="c3bb5-193">How to see the details of a portal notification</span></span>

<span data-ttu-id="c3bb5-194">You can see the details of any portal notification by following the steps below:</span><span class="sxs-lookup"><span data-stu-id="c3bb5-194">You can see the details of any portal notification by following the steps below:</span></span>

1.  <span data-ttu-id="c3bb5-195">click the **Notifications** icon (the bell) in the upper right of the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c3bb5-195">click the **Notifications** icon (the bell) in the upper right of the Azure portal</span></span>

2.  <span data-ttu-id="c3bb5-196">Select any notification in an **Error** state (those with a red (!) next to them).</span><span class="sxs-lookup"><span data-stu-id="c3bb5-196">Select any notification in an **Error** state (those with a red (!) next to them).</span></span>

  ><span data-ttu-id="c3bb5-197">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-197">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
  >
  >

3.  <span data-ttu-id="c3bb5-198">The **Notification Details** pane opens.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-198">The **Notification Details** pane opens.</span></span>

4.  <span data-ttu-id="c3bb5-199">Use the information yourself to understand more details about the problem.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-199">Use the information yourself to understand more details about the problem.</span></span>

5.  <span data-ttu-id="c3bb5-200">If you still need help, you can also share the information with a support engineer or the product group to get help with your problem.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-200">If you still need help, you can also share the information with a support engineer or the product group to get help with your problem.</span></span>

6.  <span data-ttu-id="c3bb5-201">Click the **copy** **icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-201">Click the **copy** **icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer.</span></span>

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a><span data-ttu-id="c3bb5-202">How to get help by sending notification details to a support engineer</span><span class="sxs-lookup"><span data-stu-id="c3bb5-202">How to get help by sending notification details to a support engineer</span></span>

<span data-ttu-id="c3bb5-203">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-203">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="c3bb5-204">You can **take a screenshot,** or click the **Copy error icon**, found to the right of the **Copy error** textbox.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-204">You can **take a screenshot,** or click the **Copy error icon**, found to the right of the **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="c3bb5-205">Notification Details Explained</span><span class="sxs-lookup"><span data-stu-id="c3bb5-205">Notification Details Explained</span></span>

<span data-ttu-id="c3bb5-206">The below explains more what each of the notification items means, and gives examples of each of them.</span><span class="sxs-lookup"><span data-stu-id="c3bb5-206">The below explains more what each of the notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="c3bb5-207">Essential Notification Items</span><span class="sxs-lookup"><span data-stu-id="c3bb5-207">Essential Notification Items</span></span>

-   <span data-ttu-id="c3bb5-208">**Title** – the descriptive title of the notification</span><span class="sxs-lookup"><span data-stu-id="c3bb5-208">**Title** – the descriptive title of the notification</span></span>

    -   <span data-ttu-id="c3bb5-209">Example – **Application proxy settings**</span><span class="sxs-lookup"><span data-stu-id="c3bb5-209">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="c3bb5-210">**Description** – the description of what occurred as a result of the operation</span><span class="sxs-lookup"><span data-stu-id="c3bb5-210">**Description** – the description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="c3bb5-211">Example – **Internal url entered is already being used by another application**</span><span class="sxs-lookup"><span data-stu-id="c3bb5-211">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="c3bb5-212">**Notification ID** – the unique id of the notification</span><span class="sxs-lookup"><span data-stu-id="c3bb5-212">**Notification ID** – the unique id of the notification</span></span>

    -   <span data-ttu-id="c3bb5-213">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="c3bb5-213">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="c3bb5-214">**Client Request ID** – the specific request id made by your browser</span><span class="sxs-lookup"><span data-stu-id="c3bb5-214">**Client Request ID** – the specific request id made by your browser</span></span>

    -   <span data-ttu-id="c3bb5-215">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="c3bb5-215">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="c3bb5-216">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span><span class="sxs-lookup"><span data-stu-id="c3bb5-216">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span></span>

    -   <span data-ttu-id="c3bb5-217">Example – **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="c3bb5-217">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="c3bb5-218">**Internal Transaction ID** – the internal ID used to look the error up in our systems</span><span class="sxs-lookup"><span data-stu-id="c3bb5-218">**Internal Transaction ID** – the internal ID used to look the error up in our systems</span></span>

    -   <span data-ttu-id="c3bb5-219">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="c3bb5-219">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="c3bb5-220">**UPN** – the user who performed the operation</span><span class="sxs-lookup"><span data-stu-id="c3bb5-220">**UPN** – the user who performed the operation</span></span>

    -   <span data-ttu-id="c3bb5-221">Example – **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="c3bb5-221">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="c3bb5-222">**Tenant ID** – the unique ID of the tenant that the user who performed the operation was a member of</span><span class="sxs-lookup"><span data-stu-id="c3bb5-222">**Tenant ID** – the unique ID of the tenant that the user who performed the operation was a member of</span></span>

    -   <span data-ttu-id="c3bb5-223">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="c3bb5-223">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="c3bb5-224">**User object ID** – the unique ID of the user who performed the operation</span><span class="sxs-lookup"><span data-stu-id="c3bb5-224">**User object ID** – the unique ID of the user who performed the operation</span></span>

    -   <span data-ttu-id="c3bb5-225">Example – **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="c3bb5-225">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="c3bb5-226">Detailed Notification Items</span><span class="sxs-lookup"><span data-stu-id="c3bb5-226">Detailed Notification Items</span></span>

-   <span data-ttu-id="c3bb5-227">**Display Name** – **(can be empty)** a more detailed display name for the error</span><span class="sxs-lookup"><span data-stu-id="c3bb5-227">**Display Name** – **(can be empty)** a more detailed display name for the error</span></span>

    -   <span data-ttu-id="c3bb5-228">Example \*– **Application proxy settings**</span><span class="sxs-lookup"><span data-stu-id="c3bb5-228">Example \*– **Application proxy settings**</span></span>

-   <span data-ttu-id="c3bb5-229">**Status** – the specific status of the notification</span><span class="sxs-lookup"><span data-stu-id="c3bb5-229">**Status** – the specific status of the notification</span></span>

    -   <span data-ttu-id="c3bb5-230">Example \*– **Failed**</span><span class="sxs-lookup"><span data-stu-id="c3bb5-230">Example \*– **Failed**</span></span>

-   <span data-ttu-id="c3bb5-231">**Object ID** – **(can be empty)** the object ID against which the operation was performed</span><span class="sxs-lookup"><span data-stu-id="c3bb5-231">**Object ID** – **(can be empty)** the object ID against which the operation was performed</span></span>

    -   <span data-ttu-id="c3bb5-232">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="c3bb5-232">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="c3bb5-233">**Details** – the detailed description of what occurred as a result of the operation</span><span class="sxs-lookup"><span data-stu-id="c3bb5-233">**Details** – the detailed description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="c3bb5-234">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span><span class="sxs-lookup"><span data-stu-id="c3bb5-234">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="c3bb5-235">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span><span class="sxs-lookup"><span data-stu-id="c3bb5-235">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

    -   <span data-ttu-id="c3bb5-236">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="c3bb5-236">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3bb5-237">Next steps</span><span class="sxs-lookup"><span data-stu-id="c3bb5-237">Next steps</span></span>
[<span data-ttu-id="c3bb5-238">Provide single sign-on to your apps with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="c3bb5-238">Provide single sign-on to your apps with Application Proxy</span></span>](application-proxy-configure-single-sign-on-with-kcd.md)

