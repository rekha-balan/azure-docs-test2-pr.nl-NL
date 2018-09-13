---
title: Problems signing in to an Azure AD Gallery application configured for password single sign-on | Microsoft Docs
description: Discusses problem areas that provide guidance to troubleshoot issues related to signing in to Azure AD Gallery applications configured for password single sign-on
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
ms.openlocfilehash: ef981686143299b41960e81cf827459493c868f6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855856"
---
# <a name="problems-signing-in-to-an-azure-ad-gallery-application-configured-for-password-single-sign-on"></a><span data-ttu-id="c5293-103">Problems signing in to an Azure AD Gallery application configured for password single sign-on</span><span class="sxs-lookup"><span data-stu-id="c5293-103">Problems signing in to an Azure AD Gallery application configured for password single sign-on</span></span>

<span data-ttu-id="c5293-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span><span class="sxs-lookup"><span data-stu-id="c5293-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="c5293-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c5293-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="c5293-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="c5293-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="c5293-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span><span class="sxs-lookup"><span data-stu-id="c5293-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="c5293-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span><span class="sxs-lookup"><span data-stu-id="c5293-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="c5293-109">Meeting browser requirements for the Access Panel</span><span class="sxs-lookup"><span data-stu-id="c5293-109">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="c5293-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span><span class="sxs-lookup"><span data-stu-id="c5293-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="c5293-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span><span class="sxs-lookup"><span data-stu-id="c5293-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="c5293-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span><span class="sxs-lookup"><span data-stu-id="c5293-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="c5293-113">For password-based SSO, the end user’s browsers can be:</span><span class="sxs-lookup"><span data-stu-id="c5293-113">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="c5293-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span><span class="sxs-lookup"><span data-stu-id="c5293-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="c5293-115">Chrome -- on Windows 7 or later, and on MacOS X or later</span><span class="sxs-lookup"><span data-stu-id="c5293-115">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="c5293-116">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span><span class="sxs-lookup"><span data-stu-id="c5293-116">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="c5293-117">The password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span><span class="sxs-lookup"><span data-stu-id="c5293-117">The password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="c5293-118">How to install the Access Panel Browser extension</span><span class="sxs-lookup"><span data-stu-id="c5293-118">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="c5293-119">To install the Access Panel Browser extension, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="c5293-119">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="c5293-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5293-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="c5293-121">click a **password-SSO application** in the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c5293-121">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="c5293-122">In the prompt asking to install the software, select **Install Now**.</span><span class="sxs-lookup"><span data-stu-id="c5293-122">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="c5293-123">Based on your browser you be directed to the download link.</span><span class="sxs-lookup"><span data-stu-id="c5293-123">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="c5293-124">**Add** the extension to your browser.</span><span class="sxs-lookup"><span data-stu-id="c5293-124">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="c5293-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span><span class="sxs-lookup"><span data-stu-id="c5293-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="c5293-126">Once installed, **restart** your browser session.</span><span class="sxs-lookup"><span data-stu-id="c5293-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="c5293-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span><span class="sxs-lookup"><span data-stu-id="c5293-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="c5293-128">You may also download the extension for Chrome and Firefox from the direct links below:</span><span class="sxs-lookup"><span data-stu-id="c5293-128">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="c5293-129">Chrome Access Panel Extension</span><span class="sxs-lookup"><span data-stu-id="c5293-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="c5293-130">Firefox Access Panel Extension</span><span class="sxs-lookup"><span data-stu-id="c5293-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="c5293-131">Setting up a group policy for Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="c5293-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="c5293-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span><span class="sxs-lookup"><span data-stu-id="c5293-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="c5293-133">The prerequisites include:</span><span class="sxs-lookup"><span data-stu-id="c5293-133">The prerequisites include:</span></span>

-   <span data-ttu-id="c5293-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span><span class="sxs-lookup"><span data-stu-id="c5293-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>

-   <span data-ttu-id="c5293-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span><span class="sxs-lookup"><span data-stu-id="c5293-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="c5293-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span><span class="sxs-lookup"><span data-stu-id="c5293-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="c5293-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="c5293-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="c5293-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how to configure the group policy and deploy it to users.</span><span class="sxs-lookup"><span data-stu-id="c5293-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how to configure the group policy and deploy it to users.</span></span>

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a><span data-ttu-id="c5293-139">Troubleshoot the Access Panel in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="c5293-139">Troubleshoot the Access Panel in Internet Explorer</span></span>

<span data-ttu-id="c5293-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-troubleshooting) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span><span class="sxs-lookup"><span data-stu-id="c5293-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-troubleshooting) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="c5293-141">How to configure password single sign-on for a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="c5293-141">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="c5293-142">To configure an application from the Azure AD gallery you need to:</span><span class="sxs-lookup"><span data-stu-id="c5293-142">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="c5293-143">Add a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="c5293-143">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="c5293-144">Configure the application for password single sign-on</span><span class="sxs-lookup"><span data-stu-id="c5293-144">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="c5293-145">Assign users to the application</span><span class="sxs-lookup"><span data-stu-id="c5293-145">Assign users to the application</span></span>](#assign-users-to-the-application)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="c5293-146">Add a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="c5293-146">Add a non-gallery application</span></span>

<span data-ttu-id="c5293-147">To add an application from the Azure AD Gallery, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="c5293-147">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="c5293-148">Open the [Azure portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span><span class="sxs-lookup"><span data-stu-id="c5293-148">Open the [Azure portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="c5293-149">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="c5293-149">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="c5293-150">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="c5293-150">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5293-151">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="c5293-151">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="c5293-152">click the **Add** button at the top-right corner on the **Enterprise Applications** pane.</span><span class="sxs-lookup"><span data-stu-id="c5293-152">click the **Add** button at the top-right corner on the **Enterprise Applications** pane.</span></span>

6.  <span data-ttu-id="c5293-153">click **Non-gallery application.**</span><span class="sxs-lookup"><span data-stu-id="c5293-153">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="c5293-154">Enter the name of your application in the **Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="c5293-154">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="c5293-155">Select **Add.**</span><span class="sxs-lookup"><span data-stu-id="c5293-155">Select **Add.**</span></span>

<span data-ttu-id="c5293-156">After a short period, you be able to see the application’s configuration pane.</span><span class="sxs-lookup"><span data-stu-id="c5293-156">After a short period, you be able to see the application’s configuration pane.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="c5293-157">Configure the application for password single sign-on</span><span class="sxs-lookup"><span data-stu-id="c5293-157">Configure the application for password single sign-on</span></span>

<span data-ttu-id="c5293-158">To configure single sign-on for an application, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="c5293-158">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="c5293-159">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="c5293-159">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c5293-160">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="c5293-160">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="c5293-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="c5293-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5293-162">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="c5293-162">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="c5293-163">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="c5293-163">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="c5293-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="c5293-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="c5293-165">Select the application you want to configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="c5293-165">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="c5293-166">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="c5293-166">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="c5293-167">Select the mode **Password-based Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="c5293-167">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="c5293-168">Enter the **Sign-on URL**.</span><span class="sxs-lookup"><span data-stu-id="c5293-168">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="c5293-169">This is the URL where users enter their username and password to sign in to.</span><span class="sxs-lookup"><span data-stu-id="c5293-169">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="c5293-170">Ensure the sign in fields are visible at the URL.</span><span class="sxs-lookup"><span data-stu-id="c5293-170">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="c5293-171">Assign users to the application.</span><span class="sxs-lookup"><span data-stu-id="c5293-171">Assign users to the application.</span></span>

11. <span data-ttu-id="c5293-172">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span><span class="sxs-lookup"><span data-stu-id="c5293-172">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="c5293-173">Otherwise, users be prompted to enter the credentials themselves upon launch.</span><span class="sxs-lookup"><span data-stu-id="c5293-173">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

### <a name="assign-users-to-the-application"></a><span data-ttu-id="c5293-174">Assign users to the application</span><span class="sxs-lookup"><span data-stu-id="c5293-174">Assign users to the application</span></span>

<span data-ttu-id="c5293-175">To assign one or more users to an application directly, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="c5293-175">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="c5293-176">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="c5293-176">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="c5293-177">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="c5293-177">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="c5293-178">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="c5293-178">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c5293-179">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="c5293-179">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="c5293-180">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="c5293-180">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="c5293-181">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="c5293-181">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="c5293-182">Select the application you want to assign a user to from the list.</span><span class="sxs-lookup"><span data-stu-id="c5293-182">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="c5293-183">Once the application loads, click **Users and Groups** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="c5293-183">Once the application loads, click **Users and Groups** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="c5293-184">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** pane.</span><span class="sxs-lookup"><span data-stu-id="c5293-184">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** pane.</span></span>

9.  <span data-ttu-id="c5293-185">click the **Users and groups** selector from the **Add Assignment** pane.</span><span class="sxs-lookup"><span data-stu-id="c5293-185">click the **Users and groups** selector from the **Add Assignment** pane.</span></span>

10. <span data-ttu-id="c5293-186">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span><span class="sxs-lookup"><span data-stu-id="c5293-186">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="c5293-187">Hover over the **user** in the list to reveal a **checkbox**.</span><span class="sxs-lookup"><span data-stu-id="c5293-187">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="c5293-188">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="c5293-188">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="c5293-189">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="c5293-189">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="c5293-190">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="c5293-190">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="c5293-191">**Optional:** click the **Select Role** selector in the **Add Assignment** pane to select a role to assign to the users you have selected.</span><span class="sxs-lookup"><span data-stu-id="c5293-191">**Optional:** click the **Select Role** selector in the **Add Assignment** pane to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="c5293-192">Click the **Assign** button to assign the application to the selected users.</span><span class="sxs-lookup"><span data-stu-id="c5293-192">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="c5293-193">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c5293-193">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="c5293-194">If these troubleshooting steps do not the resolve the issue</span><span class="sxs-lookup"><span data-stu-id="c5293-194">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="c5293-195">open a support ticket with the following information if available:</span><span class="sxs-lookup"><span data-stu-id="c5293-195">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="c5293-196">Correlation error ID</span><span class="sxs-lookup"><span data-stu-id="c5293-196">Correlation error ID</span></span>

-   <span data-ttu-id="c5293-197">UPN (user email address)</span><span class="sxs-lookup"><span data-stu-id="c5293-197">UPN (user email address)</span></span>

-   <span data-ttu-id="c5293-198">TenantID</span><span class="sxs-lookup"><span data-stu-id="c5293-198">TenantID</span></span>

-   <span data-ttu-id="c5293-199">Browser type</span><span class="sxs-lookup"><span data-stu-id="c5293-199">Browser type</span></span>

-   <span data-ttu-id="c5293-200">Time zone and time/timeframe during error occurs</span><span class="sxs-lookup"><span data-stu-id="c5293-200">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="c5293-201">Fiddler traces</span><span class="sxs-lookup"><span data-stu-id="c5293-201">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5293-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="c5293-202">Next steps</span></span>
[<span data-ttu-id="c5293-203">Provide single sign-on to your apps with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="c5293-203">Provide single sign-on to your apps with Application Proxy</span></span>](application-proxy-configure-single-sign-on-with-kcd.md)

