---
title: How to configure password single sign-on for a non-gallery applicationn | Microsoft Docs
description: How to configure an custom non-gallery application for secure password-based single sign-on when it is not listed in the Azure AD Application Gallery
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
ms.openlocfilehash: 37ac3b5fb680a9966f5b8f3da43a2b3013554557
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868710"
---
# <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="ad6b6-103">How to configure password single sign-on for a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="ad6b6-103">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="ad6b6-104">In addition to the choices found within the Azure AD Application Gallery, you also have the option to add a **non-gallery application** when the application you want is not listed there.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-104">In addition to the choices found within the Azure AD Application Gallery, you also have the option to add a **non-gallery application** when the application you want is not listed there.</span></span> <span data-ttu-id="ad6b6-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="ad6b6-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

<span data-ttu-id="ad6b6-106">Once you add a non-gallery application, you can then configure the Single sign-on method this application uses by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ad6b6-106">Once you add a non-gallery application, you can then configure the Single sign-on method this application uses by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="ad6b6-107">One of the Single Sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-107">One of the Single Sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="ad6b6-108">With the **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-108">With the **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span></span>

<span data-ttu-id="ad6b6-109">The way this works is by a page scraping technology that is part of the Access Panel extension that allows us to auto-detect username and password input fields, store them securely for your specific application instance.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-109">The way this works is by a page scraping technology that is part of the Access Panel extension that allows us to auto-detect username and password input fields, store them securely for your specific application instance.</span></span> <span data-ttu-id="ad6b6-110">Then securely replay usernames and passwords to those fields when a user navigates to that application on the application access panel.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-110">Then securely replay usernames and passwords to those fields when a user navigates to that application on the application access panel.</span></span>

<span data-ttu-id="ad6b6-111">This is a great way to get started integrating any kind of application into Azure AD quickly, and allows you to:</span><span class="sxs-lookup"><span data-stu-id="ad6b6-111">This is a great way to get started integrating any kind of application into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="ad6b6-112">Integrate **any application in the world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span><span class="sxs-lookup"><span data-stu-id="ad6b6-112">Integrate **any application in the world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span></span>

-   <span data-ttu-id="ad6b6-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad6b6-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="ad6b6-114">**Auto-detect input** fields for any application and allow you to manually detect those fields using the Access Panel Browser Extension, in case auto-detection does not find them</span><span class="sxs-lookup"><span data-stu-id="ad6b6-114">**Auto-detect input** fields for any application and allow you to manually detect those fields using the Access Panel Browser Extension, in case auto-detection does not find them</span></span>

-   <span data-ttu-id="ad6b6-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span><span class="sxs-lookup"><span data-stu-id="ad6b6-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span></span>

-   <span data-ttu-id="ad6b6-116">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span><span class="sxs-lookup"><span data-stu-id="ad6b6-116">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="ad6b6-117">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="ad6b6-117">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="ad6b6-118">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span><span class="sxs-lookup"><span data-stu-id="ad6b6-118">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="ad6b6-119">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#_How_to_configure_1)</span><span class="sxs-lookup"><span data-stu-id="ad6b6-119">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#_How_to_configure_1)</span></span>

-   <span data-ttu-id="ad6b6-120">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="ad6b6-120">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="ad6b6-121">The following section describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to any application that you add using the **add a non-gallery application** experience.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-121">The following section describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to any application that you add using the **add a non-gallery application** experience.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="ad6b6-122">Overview of steps required</span><span class="sxs-lookup"><span data-stu-id="ad6b6-122">Overview of steps required</span></span>

<span data-ttu-id="ad6b6-123">To configure an application from the Azure AD gallery you need to:</span><span class="sxs-lookup"><span data-stu-id="ad6b6-123">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="ad6b6-124">Add a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="ad6b6-124">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="ad6b6-125">Configure the application for password single sign-on</span><span class="sxs-lookup"><span data-stu-id="ad6b6-125">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="ad6b6-126">Assign the application to a user or a group</span><span class="sxs-lookup"><span data-stu-id="ad6b6-126">Assign the application to a user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="ad6b6-127">Assign a user to an application directly</span><span class="sxs-lookup"><span data-stu-id="ad6b6-127">Assign a user to an application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="ad6b6-128">Assign an application to a group directly</span><span class="sxs-lookup"><span data-stu-id="ad6b6-128">Assign an application to a group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a><span data-ttu-id="ad6b6-129">Add a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="ad6b6-129">Add a non-gallery application</span></span>

<span data-ttu-id="ad6b6-130">To add an application from the Azure AD Gallery, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="ad6b6-130">To add an application from the Azure AD Gallery, follow these steps:</span></span>

1.  <span data-ttu-id="ad6b6-131">Open the [Azure portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span><span class="sxs-lookup"><span data-stu-id="ad6b6-131">Open the [Azure portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="ad6b6-132">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-132">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="ad6b6-133">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-133">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ad6b6-134">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-134">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="ad6b6-135">click the **Add** button at the top-right corner on the **Enterprise Applications** pane.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-135">click the **Add** button at the top-right corner on the **Enterprise Applications** pane.</span></span>

6.  <span data-ttu-id="ad6b6-136">click **Non-gallery application**.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-136">click **Non-gallery application**.</span></span>

7.  <span data-ttu-id="ad6b6-137">Enter the name of your application in the **Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-137">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="ad6b6-138">Select **Add.**</span><span class="sxs-lookup"><span data-stu-id="ad6b6-138">Select **Add.**</span></span>

<span data-ttu-id="ad6b6-139">After a short period, you be able to see the application’s configuration pane.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-139">After a short period, you be able to see the application’s configuration pane.</span></span>

## <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="ad6b6-140">Configure the application for password single sign-on</span><span class="sxs-lookup"><span data-stu-id="ad6b6-140">Configure the application for password single sign-on</span></span>

<span data-ttu-id="ad6b6-141">To configure single sign-on for an application, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="ad6b6-141">To configure single sign-on for an application, follow these steps:</span></span>

1.  <span data-ttu-id="ad6b6-142">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="ad6b6-142">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ad6b6-143">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-143">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="ad6b6-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ad6b6-145">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-145">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="ad6b6-146">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="ad6b6-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="ad6b6-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="ad6b6-148">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-148">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="ad6b6-149">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-149">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="ad6b6-150">Select the mode **Password-based Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="ad6b6-150">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="ad6b6-151">Enter the **Sign-on URL**.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-151">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="ad6b6-152">This is the URL where users enter their username and password to sign in to.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-152">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="ad6b6-153">Ensure the sign-in fields are visible at the URL.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-153">Ensure the sign-in fields are visible at the URL.</span></span>

10. <span data-ttu-id="ad6b6-154">Assign users to the application.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-154">Assign users to the application.</span></span>

11. <span data-ttu-id="ad6b6-155">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-155">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="ad6b6-156">Otherwise, users be prompted to enter the credentials themselves upon launch.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-156">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

12. <span data-ttu-id="ad6b6-157">**Optional:** For certain social media applications like Twitter and Facebook, there is also the option to enable automatic rollover of the password for the application at a selected frequency.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-157">**Optional:** For certain social media applications like Twitter and Facebook, there is also the option to enable automatic rollover of the password for the application at a selected frequency.</span></span> <span data-ttu-id="ad6b6-158">To enable this select **I want Azure AD to automatically manage this user or group's password** while entering credentials on behalf of a user or group.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-158">To enable this select **I want Azure AD to automatically manage this user or group's password** while entering credentials on behalf of a user or group.</span></span> <span data-ttu-id="ad6b6-159">Then select the **Rollover frequency (in weeks)**.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-159">Then select the **Rollover frequency (in weeks)**.</span></span>

## <a name="assign-a-user-to-an-application-directly"></a><span data-ttu-id="ad6b6-160">Assign a user to an application directly</span><span class="sxs-lookup"><span data-stu-id="ad6b6-160">Assign a user to an application directly</span></span>

<span data-ttu-id="ad6b6-161">To assign one or more users to an application directly, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="ad6b6-161">To assign one or more users to an application directly, follow these steps:</span></span>

1.  <span data-ttu-id="ad6b6-162">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="ad6b6-162">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="ad6b6-163">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-163">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="ad6b6-164">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-164">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ad6b6-165">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-165">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="ad6b6-166">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-166">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="ad6b6-167">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="ad6b6-167">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="ad6b6-168">Select the application you want to assign a user to from the list.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-168">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="ad6b6-169">Once the application loads, click **Users and Groups** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-169">Once the application loads, click **Users and Groups** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="ad6b6-170">To open the **Add Assignment** pane, click the **Add** button on top of the **Users and Groups** list.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-170">To open the **Add Assignment** pane, click the **Add** button on top of the **Users and Groups** list.</span></span>

9.  <span data-ttu-id="ad6b6-171">click the **Users and groups** selector from the **Add Assignment** pane.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-171">click the **Users and groups** selector from the **Add Assignment** pane.</span></span>

10. <span data-ttu-id="ad6b6-172">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-172">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="ad6b6-173">Hover over the **user** in the list to reveal a **checkbox**.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-173">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="ad6b6-174">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-174">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="ad6b6-175">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-175">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="ad6b6-176">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-176">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="ad6b6-177">**Optional:** click the **Select Role** selector in the **Add Assignment** pane to select a role to assign to the users you have selected.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-177">**Optional:** click the **Select Role** selector in the **Add Assignment** pane to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="ad6b6-178">Click the **Assign** button to assign the application to the selected users.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-178">Click the **Assign** button to assign the application to the selected users.</span></span>

## <a name="assign-an-application-to-a-group-directly"></a><span data-ttu-id="ad6b6-179">Assign an application to a group directly</span><span class="sxs-lookup"><span data-stu-id="ad6b6-179">Assign an application to a group directly</span></span>

<span data-ttu-id="ad6b6-180">To assign one or more groups to an application directly, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="ad6b6-180">To assign one or more groups to an application directly, follow these steps:</span></span>

1.  <span data-ttu-id="ad6b6-181">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="ad6b6-181">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="ad6b6-182">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-182">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="ad6b6-183">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-183">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ad6b6-184">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-184">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="ad6b6-185">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-185">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="ad6b6-186">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="ad6b6-186">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="ad6b6-187">Select the application you want to assign a user to from the list.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-187">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="ad6b6-188">Once the application loads, click **Users and Groups** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-188">Once the application loads, click **Users and Groups** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="ad6b6-189">To open the **Add Assignment** pane, click the **Add** button on top of the **Users and Groups** list.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-189">To open the **Add Assignment** pane, click the **Add** button on top of the **Users and Groups** list.</span></span>

9.  <span data-ttu-id="ad6b6-190">click the **Users and groups** selector from the **Add Assignment** pane.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-190">click the **Users and groups** selector from the **Add Assignment** pane.</span></span>

10. <span data-ttu-id="ad6b6-191">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-191">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="ad6b6-192">Hover over the **group** in the list to reveal a **checkbox**.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-192">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="ad6b6-193">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-193">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="ad6b6-194">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-194">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="ad6b6-195">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-195">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="ad6b6-196">**Optional:** click the **Select Role** selector in the **Add Assignment** pane to select a role to assign to the groups you have selected.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-196">**Optional:** click the **Select Role** selector in the **Add Assignment** pane to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="ad6b6-197">Click the **Assign** button to assign the application to the selected groups.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-197">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="ad6b6-198">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ad6b6-198">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad6b6-199">Next steps</span><span class="sxs-lookup"><span data-stu-id="ad6b6-199">Next steps</span></span>
[<span data-ttu-id="ad6b6-200">Provide single sign-on to your apps with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="ad6b6-200">Provide single sign-on to your apps with Application Proxy</span></span>](application-proxy-configure-single-sign-on-with-kcd.md)
