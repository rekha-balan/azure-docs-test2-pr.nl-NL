---
title: How to configure password single sign-on for an Azure AD Gallery application | Microsoft Docs
description: How to configure an application for secure password-based single sign-on when it is already listed in the Azure AD Application Gallery
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
ms.openlocfilehash: 7293e0ea79f0a263cb55f81770f5f6aef28a0f40
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670295"
---
# <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="cfcd0-103">How to configure password single sign-on for an Azure AD Gallery application</span><span class="sxs-lookup"><span data-stu-id="cfcd0-103">How to configure password single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="cfcd0-104">When you add an application from the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), you have the choice of how you want your users to sign in to that application.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-104">When you add an application from the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), you have the choice of how you want your users to sign in to that application.</span></span> <span data-ttu-id="cfcd0-105">You can configure this choice at any time by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cfcd0-105">You can configure this choice at any time by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="cfcd0-106">One of the single sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-106">One of the single sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="cfcd0-107">This is a great way to get started integrating applications into Azure AD quickly, and allows you to:</span><span class="sxs-lookup"><span data-stu-id="cfcd0-107">This is a great way to get started integrating applications into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="cfcd0-108">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span><span class="sxs-lookup"><span data-stu-id="cfcd0-108">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="cfcd0-109">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span><span class="sxs-lookup"><span data-stu-id="cfcd0-109">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span></span>

-   <span data-ttu-id="cfcd0-110">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span><span class="sxs-lookup"><span data-stu-id="cfcd0-110">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="cfcd0-111">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="cfcd0-111">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="cfcd0-112">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span><span class="sxs-lookup"><span data-stu-id="cfcd0-112">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="cfcd0-113">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#assign-a-user-to-an-application-directly)</span><span class="sxs-lookup"><span data-stu-id="cfcd0-113">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#assign-a-user-to-an-application-directly)</span></span>

-   <span data-ttu-id="cfcd0-114">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="cfcd0-114">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="cfcd0-115">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to an application that is already in the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="cfcd0-115">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to an application that is already in the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="cfcd0-116">Overview of steps required</span><span class="sxs-lookup"><span data-stu-id="cfcd0-116">Overview of steps required</span></span>
<span data-ttu-id="cfcd0-117">To configure an application from the Azure AD gallery you need to:</span><span class="sxs-lookup"><span data-stu-id="cfcd0-117">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="cfcd0-118">Add an application from the Azure AD gallery</span><span class="sxs-lookup"><span data-stu-id="cfcd0-118">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="cfcd0-119">Configure the application for password single sign-on</span><span class="sxs-lookup"><span data-stu-id="cfcd0-119">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="cfcd0-120">Assign the application to a user or a group</span><span class="sxs-lookup"><span data-stu-id="cfcd0-120">Assign the application to a user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="cfcd0-121">Assign a user to an application directly</span><span class="sxs-lookup"><span data-stu-id="cfcd0-121">Assign a user to an application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="cfcd0-122">Assign an application to a group directly</span><span class="sxs-lookup"><span data-stu-id="cfcd0-122">Assign an application to a group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="cfcd0-123">Add an application from the Azure AD gallery</span><span class="sxs-lookup"><span data-stu-id="cfcd0-123">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="cfcd0-124">To add an application from the Azure AD Gallery, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="cfcd0-124">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="cfcd0-125">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span><span class="sxs-lookup"><span data-stu-id="cfcd0-125">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="cfcd0-126">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-126">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="cfcd0-127">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-127">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="cfcd0-128">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-128">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="cfcd0-129">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span><span class="sxs-lookup"><span data-stu-id="cfcd0-129">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="cfcd0-130">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application</span><span class="sxs-lookup"><span data-stu-id="cfcd0-130">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application</span></span>

7.  <span data-ttu-id="cfcd0-131">Select the application you want to configure for single sign-on</span><span class="sxs-lookup"><span data-stu-id="cfcd0-131">Select the application you want to configure for single sign-on</span></span>

8.  <span data-ttu-id="cfcd0-132">Before adding the application, you can change its name from the **Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-132">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="cfcd0-133">Click **Add** button, to add the application.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-133">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="cfcd0-134">After a short period, you be able to see the application’s configuration blade.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-134">After a short period, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="cfcd0-135">Configure the application for password single sign-on</span><span class="sxs-lookup"><span data-stu-id="cfcd0-135">Configure the application for password single sign-on</span></span>

<span data-ttu-id="cfcd0-136">To configure single sign-on for an application, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="cfcd0-136">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="cfcd0-137">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="cfcd0-137">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="cfcd0-138">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-138">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="cfcd0-139">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-139">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="cfcd0-140">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-140">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="cfcd0-141">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-141">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="cfcd0-142">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="cfcd0-142">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="cfcd0-143">Select the application you want to configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="cfcd0-143">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="cfcd0-144">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-144">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="cfcd0-145">Select the mode **Password-based Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="cfcd0-145">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="cfcd0-146">[Assign users to the application](#assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="cfcd0-146">[Assign users to the application](#assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="cfcd0-147">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-147">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="cfcd0-148">Otherwise, users be prompted to enter the credentials themselves upon launch.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-148">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="assign-a-user-to-an-application-directly"></a><span data-ttu-id="cfcd0-149">Assign a user to an application directly</span><span class="sxs-lookup"><span data-stu-id="cfcd0-149">Assign a user to an application directly</span></span>

<span data-ttu-id="cfcd0-150">To assign one or more users to an application directly, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="cfcd0-150">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="cfcd0-151">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="cfcd0-151">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="cfcd0-152">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-152">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="cfcd0-153">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-153">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="cfcd0-154">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-154">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="cfcd0-155">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-155">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="cfcd0-156">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="cfcd0-156">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="cfcd0-157">Select the application you want to assign a user to from the list.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-157">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="cfcd0-158">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-158">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="cfcd0-159">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-159">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="cfcd0-160">click the **Users and groups** selector from the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-160">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="cfcd0-161">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-161">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="cfcd0-162">Hover over the **user** in the list to reveal a **checkbox**.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-162">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="cfcd0-163">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-163">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="cfcd0-164">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-164">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="cfcd0-165">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-165">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="cfcd0-166">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-166">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="cfcd0-167">Click the **Assign** button to assign the application to the selected users.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-167">Click the **Assign** button to assign the application to the selected users.</span></span>

## <a name="assign-an-application-to-a-group-directly"></a><span data-ttu-id="cfcd0-168">Assign an application to a group directly</span><span class="sxs-lookup"><span data-stu-id="cfcd0-168">Assign an application to a group directly</span></span>

<span data-ttu-id="cfcd0-169">To assign one or more groups to an application directly, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="cfcd0-169">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="cfcd0-170">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="cfcd0-170">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="cfcd0-171">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-171">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="cfcd0-172">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-172">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="cfcd0-173">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-173">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="cfcd0-174">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-174">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="cfcd0-175">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="cfcd0-175">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="cfcd0-176">Select the application you want to assign a user to from the list.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-176">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="cfcd0-177">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-177">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="cfcd0-178">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-178">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="cfcd0-179">click the **Users and groups** selector from the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-179">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="cfcd0-180">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-180">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="cfcd0-181">Hover over the **group** in the list to reveal a **checkbox**.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-181">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="cfcd0-182">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-182">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="cfcd0-183">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-183">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="cfcd0-184">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-184">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="cfcd0-185">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-185">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="cfcd0-186">Click the **Assign** button to assign the application to the selected groups.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-186">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="cfcd0-187">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="cfcd0-187">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfcd0-188">Next steps</span><span class="sxs-lookup"><span data-stu-id="cfcd0-188">Next steps</span></span>
[<span data-ttu-id="cfcd0-189">Provide single sign-on to your apps with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="cfcd0-189">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
