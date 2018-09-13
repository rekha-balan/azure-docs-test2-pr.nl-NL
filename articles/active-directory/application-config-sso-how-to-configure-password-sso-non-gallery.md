---
title: How to configure password single sign-on for a non-gallery applicationn | Microsoft Docs
description: How to configure an custom non-gallery application for secure password-based single sign-on when it is not listed in the Azure AD Application Gallery
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
ms.openlocfilehash: 9826c4d377ca79f5551ac574b42d52c3067db802
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556622"
---
# <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="42aff-103">How to configure password single sign-on for a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="42aff-103">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="42aff-104">In addition to the choices found within the Azure AD Application Gallery, you also have the option to add a **non-gallery application** when the application you want is not listed there.</span><span class="sxs-lookup"><span data-stu-id="42aff-104">In addition to the choices found within the Azure AD Application Gallery, you also have the option to add a **non-gallery application** when the application you want is not listed there.</span></span> <span data-ttu-id="42aff-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="42aff-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

<span data-ttu-id="42aff-106">Once you add a non-gallery application, you can then configure the Single sign-on method this application uses by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="42aff-106">Once you add a non-gallery application, you can then configure the Single sign-on method this application uses by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="42aff-107">One of the Single Sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span><span class="sxs-lookup"><span data-stu-id="42aff-107">One of the Single Sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="42aff-108">With the **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span><span class="sxs-lookup"><span data-stu-id="42aff-108">With the **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span></span>

<span data-ttu-id="42aff-109">The way this works is by a page scraping technology that is part of the Access Panel extension that allows us to auto-detect username and password input fields, store them securely for your specific application instance.</span><span class="sxs-lookup"><span data-stu-id="42aff-109">The way this works is by a page scraping technology that is part of the Access Panel extension that allows us to auto-detect username and password input fields, store them securely for your specific application instance.</span></span> <span data-ttu-id="42aff-110">Then securely replay usernames and passwords to those fields when a user navigates to that application on the application access panel.</span><span class="sxs-lookup"><span data-stu-id="42aff-110">Then securely replay usernames and passwords to those fields when a user navigates to that application on the application access panel.</span></span>

<span data-ttu-id="42aff-111">This is a great way to get started integrating any kind of application into Azure AD quickly, and allows you to:</span><span class="sxs-lookup"><span data-stu-id="42aff-111">This is a great way to get started integrating any kind of application into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="42aff-112">Integrate **any application in the world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span><span class="sxs-lookup"><span data-stu-id="42aff-112">Integrate **any application in the world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span></span>

-   <span data-ttu-id="42aff-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span><span class="sxs-lookup"><span data-stu-id="42aff-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="42aff-114">**Auto-detect input** fields for any application and allow you to manually detect those fields using the Access Panel Browser Extension, in case auto-detection does not find them</span><span class="sxs-lookup"><span data-stu-id="42aff-114">**Auto-detect input** fields for any application and allow you to manually detect those fields using the Access Panel Browser Extension, in case auto-detection does not find them</span></span>

-   <span data-ttu-id="42aff-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span><span class="sxs-lookup"><span data-stu-id="42aff-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span></span>

-   <span data-ttu-id="42aff-116">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span><span class="sxs-lookup"><span data-stu-id="42aff-116">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="42aff-117">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="42aff-117">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="42aff-118">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span><span class="sxs-lookup"><span data-stu-id="42aff-118">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="42aff-119">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#_How_to_configure_1)</span><span class="sxs-lookup"><span data-stu-id="42aff-119">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#_How_to_configure_1)</span></span>

-   <span data-ttu-id="42aff-120">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="42aff-120">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="42aff-121">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to any application that you add using the **add a non-gallery application** experience.</span><span class="sxs-lookup"><span data-stu-id="42aff-121">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to any application that you add using the **add a non-gallery application** experience.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="42aff-122">Overview of steps required</span><span class="sxs-lookup"><span data-stu-id="42aff-122">Overview of steps required</span></span>

<span data-ttu-id="42aff-123">To configure an application from the Azure AD gallery you need to:</span><span class="sxs-lookup"><span data-stu-id="42aff-123">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="42aff-124">Add a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="42aff-124">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="42aff-125">Configure the application for password single sign-on</span><span class="sxs-lookup"><span data-stu-id="42aff-125">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="42aff-126">Assign the application to a user or a group</span><span class="sxs-lookup"><span data-stu-id="42aff-126">Assign the application to a user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="42aff-127">Assign a user to an application directly</span><span class="sxs-lookup"><span data-stu-id="42aff-127">Assign a user to an application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="42aff-128">Assign an application to a group directly</span><span class="sxs-lookup"><span data-stu-id="42aff-128">Assign an application to a group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a><span data-ttu-id="42aff-129">Add a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="42aff-129">Add a non-gallery application</span></span>

<span data-ttu-id="42aff-130">To add an application from the Azure AD Gallery, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="42aff-130">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="42aff-131">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span><span class="sxs-lookup"><span data-stu-id="42aff-131">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="42aff-132">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="42aff-132">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="42aff-133">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="42aff-133">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="42aff-134">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="42aff-134">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="42aff-135">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span><span class="sxs-lookup"><span data-stu-id="42aff-135">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="42aff-136">click **Non-gallery application.**</span><span class="sxs-lookup"><span data-stu-id="42aff-136">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="42aff-137">Enter the name of your application in the **Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="42aff-137">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="42aff-138">Select **Add.**</span><span class="sxs-lookup"><span data-stu-id="42aff-138">Select **Add.**</span></span>

<span data-ttu-id="42aff-139">After a short period, you be able to see the application’s configuration blade.</span><span class="sxs-lookup"><span data-stu-id="42aff-139">After a short period, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="42aff-140">Configure the application for password single sign-on</span><span class="sxs-lookup"><span data-stu-id="42aff-140">Configure the application for password single sign-on</span></span>

<span data-ttu-id="42aff-141">To configure single sign-on for an application, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="42aff-141">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="42aff-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="42aff-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="42aff-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="42aff-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="42aff-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="42aff-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="42aff-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="42aff-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="42aff-146">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="42aff-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="42aff-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="42aff-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="42aff-148">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="42aff-148">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="42aff-149">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="42aff-149">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="42aff-150">Select the mode **Password-based Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="42aff-150">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="42aff-151">Enter the **Sign-on URL**.</span><span class="sxs-lookup"><span data-stu-id="42aff-151">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="42aff-152">This is the URL where users enter their username and password to sign in to.</span><span class="sxs-lookup"><span data-stu-id="42aff-152">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="42aff-153">Ensure the sign in fields are visible at the URL.</span><span class="sxs-lookup"><span data-stu-id="42aff-153">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="42aff-154">Assign users to the application.</span><span class="sxs-lookup"><span data-stu-id="42aff-154">Assign users to the application.</span></span>

11. <span data-ttu-id="42aff-155">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span><span class="sxs-lookup"><span data-stu-id="42aff-155">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="42aff-156">Otherwise, users be prompted to enter the credentials themselves upon launch.</span><span class="sxs-lookup"><span data-stu-id="42aff-156">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="assign-a-user-to-an-application-directly"></a><span data-ttu-id="42aff-157">Assign a user to an application directly</span><span class="sxs-lookup"><span data-stu-id="42aff-157">Assign a user to an application directly</span></span>

<span data-ttu-id="42aff-158">To assign one or more users to an application directly, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="42aff-158">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="42aff-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="42aff-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="42aff-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="42aff-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="42aff-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="42aff-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="42aff-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="42aff-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="42aff-163">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="42aff-163">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="42aff-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="42aff-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="42aff-165">Select the application you want to assign a user to from the list.</span><span class="sxs-lookup"><span data-stu-id="42aff-165">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="42aff-166">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="42aff-166">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="42aff-167">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="42aff-167">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="42aff-168">click the **Users and groups** selector from the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="42aff-168">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="42aff-169">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span><span class="sxs-lookup"><span data-stu-id="42aff-169">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="42aff-170">Hover over the **user** in the list to reveal a **checkbox**.</span><span class="sxs-lookup"><span data-stu-id="42aff-170">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="42aff-171">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="42aff-171">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="42aff-172">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="42aff-172">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="42aff-173">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="42aff-173">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="42aff-174">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span><span class="sxs-lookup"><span data-stu-id="42aff-174">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="42aff-175">Click the **Assign** button to assign the application to the selected users.</span><span class="sxs-lookup"><span data-stu-id="42aff-175">Click the **Assign** button to assign the application to the selected users.</span></span>

## <a name="assign-an-application-to-a-group-directly"></a><span data-ttu-id="42aff-176">Assign an application to a group directly</span><span class="sxs-lookup"><span data-stu-id="42aff-176">Assign an application to a group directly</span></span>

<span data-ttu-id="42aff-177">To assign one or more groups to an application directly, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="42aff-177">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="42aff-178">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="42aff-178">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="42aff-179">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="42aff-179">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="42aff-180">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="42aff-180">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="42aff-181">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="42aff-181">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="42aff-182">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="42aff-182">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="42aff-183">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="42aff-183">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="42aff-184">Select the application you want to assign a user to from the list.</span><span class="sxs-lookup"><span data-stu-id="42aff-184">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="42aff-185">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="42aff-185">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="42aff-186">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="42aff-186">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="42aff-187">click the **Users and groups** selector from the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="42aff-187">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="42aff-188">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span><span class="sxs-lookup"><span data-stu-id="42aff-188">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="42aff-189">Hover over the **group** in the list to reveal a **checkbox**.</span><span class="sxs-lookup"><span data-stu-id="42aff-189">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="42aff-190">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="42aff-190">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="42aff-191">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="42aff-191">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="42aff-192">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="42aff-192">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="42aff-193">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span><span class="sxs-lookup"><span data-stu-id="42aff-193">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="42aff-194">Click the **Assign** button to assign the application to the selected groups.</span><span class="sxs-lookup"><span data-stu-id="42aff-194">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="42aff-195">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="42aff-195">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42aff-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="42aff-196">Next steps</span></span>
[<span data-ttu-id="42aff-197">Provide single sign-on to your apps with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="42aff-197">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
