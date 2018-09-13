---
title: Problems signing in to an application from the access panel | Microsoft Docs
description: How to troubleshoot issues accessing an application from the Microsoft Azure AD Access Panel at myapps.microsoft.com
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
ms.reviewer: japere
ms.openlocfilehash: 830fc1d96825e28aad41aac9afee499b9bc1f7ae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856063"
---
# <a name="problems-signing-in-to-an-application-from-the-access-panel"></a><span data-ttu-id="9ad8a-103">Problems signing in to an application from the access panel</span><span class="sxs-lookup"><span data-stu-id="9ad8a-103">Problems signing in to an application from the access panel</span></span>

<span data-ttu-id="9ad8a-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="9ad8a-105">These applications are configured on behalf of the user in the Azure AD portal.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="9ad8a-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="9ad8a-107">The type of apps a user may be seeing fall in the following categories:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-107">The type of apps a user may be seeing fall in the following categories:</span></span>

-   <span data-ttu-id="9ad8a-108">Office 365 Applications</span><span class="sxs-lookup"><span data-stu-id="9ad8a-108">Office 365 Applications</span></span>

-   <span data-ttu-id="9ad8a-109">Microsoft and third-party applications configured with federation-based SSO</span><span class="sxs-lookup"><span data-stu-id="9ad8a-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="9ad8a-110">Password-based SSO applications</span><span class="sxs-lookup"><span data-stu-id="9ad8a-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="9ad8a-111">Applications with existing SSO solutions</span><span class="sxs-lookup"><span data-stu-id="9ad8a-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="9ad8a-112">General issues to check first</span><span class="sxs-lookup"><span data-stu-id="9ad8a-112">General issues to check first</span></span>

-   <span data-ttu-id="9ad8a-113">Make sure your using a **browser** that meets the minimum requirements for the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-113">Make sure your using a **browser** that meets the minimum requirements for the Access Panel.</span></span>

-   <span data-ttu-id="9ad8a-114">Make sure the user’s browser has added the URL of the application to its **trusted sites**.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-114">Make sure the user’s browser has added the URL of the application to its **trusted sites**.</span></span>

-   <span data-ttu-id="9ad8a-115">Make sure to check the application is **configured** correctly.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-115">Make sure to check the application is **configured** correctly.</span></span>

-   <span data-ttu-id="9ad8a-116">Make sure the user’s account is **enabled** for sign-ins.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-116">Make sure the user’s account is **enabled** for sign-ins.</span></span>

-   <span data-ttu-id="9ad8a-117">Make sure the user’s account is **not locked out.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-117">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="9ad8a-118">Make sure the user’s **password is not expired or forgotten.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-118">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="9ad8a-119">Make sure **Multi-Factor Authentication** is not blocking user access.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-119">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="9ad8a-120">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-120">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="9ad8a-121">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-121">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="9ad8a-122">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-122">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="9ad8a-123">Meeting browser requirements for the Access Panel</span><span class="sxs-lookup"><span data-stu-id="9ad8a-123">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="9ad8a-124">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-124">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="9ad8a-125">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-125">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="9ad8a-126">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-126">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="9ad8a-127">For password-based SSO, the end user’s browsers can be:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-127">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="9ad8a-128">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span><span class="sxs-lookup"><span data-stu-id="9ad8a-128">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="9ad8a-129">Edge on Windows 10 Anniversary Edition or later</span><span class="sxs-lookup"><span data-stu-id="9ad8a-129">Edge on Windows 10 Anniversary Edition or later</span></span>

-   <span data-ttu-id="9ad8a-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span><span class="sxs-lookup"><span data-stu-id="9ad8a-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="9ad8a-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span><span class="sxs-lookup"><span data-stu-id="9ad8a-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="9ad8a-132">How to install the Access Panel Browser extension</span><span class="sxs-lookup"><span data-stu-id="9ad8a-132">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="9ad8a-133">To install the Access Panel Browser extension, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-133">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="9ad8a-134">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-134">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="9ad8a-135">Click a **password-SSO application** in the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-135">Click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="9ad8a-136">In the prompt asking to install the software, select **Install Now**.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-136">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="9ad8a-137">Based on your browser you are directed to the download link.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-137">Based on your browser you are directed to the download link.</span></span> <span data-ttu-id="9ad8a-138">**Add** the extension to your browser.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-138">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="9ad8a-139">If your browser asks, select to either **Enable** or **Allow** the extension.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-139">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="9ad8a-140">Once installed, **restart** your browser session.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-140">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="9ad8a-141">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span><span class="sxs-lookup"><span data-stu-id="9ad8a-141">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="9ad8a-142">You may also download the extension for Chrome and Edge from the direct links below:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-142">You may also download the extension for Chrome and Edge from the direct links below:</span></span>

-   [<span data-ttu-id="9ad8a-143">Chrome Access Panel Extension</span><span class="sxs-lookup"><span data-stu-id="9ad8a-143">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="9ad8a-144">Edge Access Panel Extension</span><span class="sxs-lookup"><span data-stu-id="9ad8a-144">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="9ad8a-145">How to configure federated single sign-on for an Azure AD gallery application</span><span class="sxs-lookup"><span data-stu-id="9ad8a-145">How to configure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="9ad8a-146">All application in the Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-146">All application in the Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="9ad8a-147">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-147">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="9ad8a-148">To configure an application from the Azure AD gallery you need to:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-148">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="9ad8a-149">Add an application from the Azure AD gallery</span><span class="sxs-lookup"><span data-stu-id="9ad8a-149">Add an application from the Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="9ad8a-150">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span><span class="sxs-lookup"><span data-stu-id="9ad8a-150">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="9ad8a-151">Select User Identifier and add user attributes to be sent to the application</span><span class="sxs-lookup"><span data-stu-id="9ad8a-151">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="9ad8a-152">Retrieve Azure AD metadata and certificate</span><span class="sxs-lookup"><span data-stu-id="9ad8a-152">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="9ad8a-153">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span><span class="sxs-lookup"><span data-stu-id="9ad8a-153">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="9ad8a-154">Assign users to the application</span><span class="sxs-lookup"><span data-stu-id="9ad8a-154">Assign users to the application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="9ad8a-155">Add an application from the Azure AD gallery</span><span class="sxs-lookup"><span data-stu-id="9ad8a-155">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="9ad8a-156">To add an application from the Azure AD Gallery, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-156">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="9ad8a-157">Open the [Azure portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-157">Open the [Azure portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="9ad8a-158">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-158">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="9ad8a-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ad8a-160">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-160">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="9ad8a-161">click the **Add** button at the top-right corner on the **Enterprise Applications** pane.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-161">click the **Add** button at the top-right corner on the **Enterprise Applications** pane.</span></span>

6.  <span data-ttu-id="9ad8a-162">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-162">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="9ad8a-163">Select the application you want to configure for single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-163">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="9ad8a-164">Before adding the application, you can change its name from the **Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-164">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="9ad8a-165">Click **Add** button, to add the application.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-165">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="9ad8a-166">After a short period, you can see the application’s configuration pane.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-166">After a short period, you can see the application’s configuration pane.</span></span>

### <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="9ad8a-167">Configure single sign-on for an application from the Azure AD gallery</span><span class="sxs-lookup"><span data-stu-id="9ad8a-167">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="9ad8a-168">To configure single sign-on for an application, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-168">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="9ad8a-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9ad8a-170">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-170">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="9ad8a-171">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-171">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ad8a-172">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-172">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="9ad8a-173">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-173">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9ad8a-174">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-174">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9ad8a-175">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-175">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="9ad8a-176">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-176">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="9ad8a-177">Select **SAML-based Sign-on** from the **Mode** dropdown.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-177">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="9ad8a-178">Enter the required values in **Domain and URLs.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-178">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="9ad8a-179">You should get these values from the application vendor.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-179">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="9ad8a-180">To configure the application as SP-initiated SSO, the Sign-on URL is a required value.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-180">To configure the application as SP-initiated SSO, the Sign-on URL is a required value.</span></span> <span data-ttu-id="9ad8a-181">For some applications, the Identifier is also a required value.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-181">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="9ad8a-182">To configure the application as IdP-initiated SSO, the Reply URL is a required value.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-182">To configure the application as IdP-initiated SSO, the Reply URL is a required value.</span></span> <span data-ttu-id="9ad8a-183">For some applications, the Identifier is also a required value.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-183">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="9ad8a-184">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-184">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="9ad8a-185">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-185">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="9ad8a-186">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when users sign in.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-186">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when users sign in.</span></span>

   <span data-ttu-id="9ad8a-187">To add an attribute:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-187">To add an attribute:</span></span>

   1. <span data-ttu-id="9ad8a-188">click **Add attribute**.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-188">click **Add attribute**.</span></span> <span data-ttu-id="9ad8a-189">Enter the **Name** and the select the **Value** from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-189">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="9ad8a-190">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-190">Click **Save.**</span></span> <span data-ttu-id="9ad8a-191">You see the new attribute in the table.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-191">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="9ad8a-192">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-192">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="9ad8a-193">Also, you have the metadata URLs and certificate required to setup SSO with the application.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-193">Also, you have the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="9ad8a-194">Click **Save** to save the configuration.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-194">Click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="9ad8a-195">Assign users to the application.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-195">Assign users to the application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="9ad8a-196">Select User Identifier and add user attributes to be sent to the application</span><span class="sxs-lookup"><span data-stu-id="9ad8a-196">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="9ad8a-197">To select the User Identifier or add user attributes, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-197">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="9ad8a-198">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-198">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9ad8a-199">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-199">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="9ad8a-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ad8a-201">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-201">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="9ad8a-202">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-202">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9ad8a-203">If you do not see the application you want to show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-203">If you do not see the application you want to show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9ad8a-204">Select the application you have configured single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-204">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="9ad8a-205">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-205">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="9ad8a-206">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-206">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="9ad8a-207">The selected option needs to match the expected value in the application to authenticate the user.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-207">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

    >[!NOTE]
    ><span data-ttu-id="9ad8a-208">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-208">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="9ad8a-209">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-209">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
    >
    >

9.  <span data-ttu-id="9ad8a-210">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when users sign in.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-210">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when users sign in.</span></span>

   <span data-ttu-id="9ad8a-211">To add an attribute:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-211">To add an attribute:</span></span>

   1. <span data-ttu-id="9ad8a-212">click **Add attribute**.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-212">click **Add attribute**.</span></span> <span data-ttu-id="9ad8a-213">Enter the **Name** and the select the **Value** from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-213">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="9ad8a-214">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-214">Click **Save.**</span></span> <span data-ttu-id="9ad8a-215">You see the new attribute in the table.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-215">You see the new attribute in the table.</span></span>

### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="9ad8a-216">Download the Azure AD metadata or certificate</span><span class="sxs-lookup"><span data-stu-id="9ad8a-216">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="9ad8a-217">To download the application metadata or certificate from Azure AD, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-217">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="9ad8a-218">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-218">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9ad8a-219">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-219">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="9ad8a-220">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-220">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ad8a-221">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-221">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="9ad8a-222">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-222">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9ad8a-223">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-223">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9ad8a-224">Select the application you have configured single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-224">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="9ad8a-225">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-225">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="9ad8a-226">Go to **SAML Signing Certificate** section, then click **Download** column value.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-226">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="9ad8a-227">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-227">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="9ad8a-228">Azure AD doesn’t provide a URL to get the metadata.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-228">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="9ad8a-229">The metadata can only be retrieved as an XML file.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-229">The metadata can only be retrieved as an XML file.</span></span>

## <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="9ad8a-230">How to configure federated single sign-on for a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="9ad8a-230">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="9ad8a-231">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-231">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="9ad8a-232">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="9ad8a-232">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="9ad8a-233">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span><span class="sxs-lookup"><span data-stu-id="9ad8a-233">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="9ad8a-234">Select User Identifier and add user attributes to be sent to the application</span><span class="sxs-lookup"><span data-stu-id="9ad8a-234">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="9ad8a-235">Retrieve Azure AD metadata and certificate</span><span class="sxs-lookup"><span data-stu-id="9ad8a-235">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="9ad8a-236">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span><span class="sxs-lookup"><span data-stu-id="9ad8a-236">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

### <a name="configure-the-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="9ad8a-237">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span><span class="sxs-lookup"><span data-stu-id="9ad8a-237">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="9ad8a-238">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-238">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="9ad8a-239">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-239">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9ad8a-240">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-240">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="9ad8a-241">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-241">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ad8a-242">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-242">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="9ad8a-243">click the **Add** button at the top-right corner on the **Enterprise Applications** pane.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-243">click the **Add** button at the top-right corner on the **Enterprise Applications** pane.</span></span>

6.  <span data-ttu-id="9ad8a-244">click **Non-gallery application** in the **Add your own app** section.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-244">click **Non-gallery application** in the **Add your own app** section.</span></span>

7.  <span data-ttu-id="9ad8a-245">Enter the name of the application in the **Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-245">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="9ad8a-246">Click **Add** button, to add the application.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-246">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="9ad8a-247">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-247">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

10. <span data-ttu-id="9ad8a-248">Select **SAML-based Sign-on** in the **Mode** dropdown</span><span class="sxs-lookup"><span data-stu-id="9ad8a-248">Select **SAML-based Sign-on** in the **Mode** dropdown</span></span>

11. <span data-ttu-id="9ad8a-249">Enter the required values in **Domain and URLs.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-249">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="9ad8a-250">You should get these values from the application vendor.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-250">You should get these values from the application vendor.</span></span>

  1. <span data-ttu-id="9ad8a-251">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-251">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

  2. <span data-ttu-id="9ad8a-252">**Optional:** To configure the application as SP-initiated SSO, the Sign-on URL is a required value.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-252">**Optional:** To configure the application as SP-initiated SSO, the Sign-on URL is a required value.</span></span>

12. <span data-ttu-id="9ad8a-253">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-253">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="9ad8a-254">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when users sign in.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-254">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when users sign in.</span></span>

   <span data-ttu-id="9ad8a-255">To add an attribute:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-255">To add an attribute:</span></span>

   1. <span data-ttu-id="9ad8a-256">click **Add attribute**.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-256">click **Add attribute**.</span></span> <span data-ttu-id="9ad8a-257">Enter the **Name** and the select the **Value** from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-257">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="9ad8a-258">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-258">Click **Save.**</span></span> <span data-ttu-id="9ad8a-259">You see the new attribute in the table.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-259">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="9ad8a-260">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-260">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="9ad8a-261">Also, you have Azure AD URLs and certificate required for the application.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-261">Also, you have Azure AD URLs and certificate required for the application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="9ad8a-262">Select User Identifier and add user attributes to be sent to the application</span><span class="sxs-lookup"><span data-stu-id="9ad8a-262">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="9ad8a-263">To select the User Identifier or add user attributes, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-263">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="9ad8a-264">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-264">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9ad8a-265">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-265">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="9ad8a-266">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-266">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ad8a-267">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-267">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="9ad8a-268">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-268">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9ad8a-269">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-269">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9ad8a-270">Select the application you have configured single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-270">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="9ad8a-271">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-271">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="9ad8a-272">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-272">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="9ad8a-273">The selected option needs to match the expected value in the application to authenticate the user.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-273">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE]
   ><span data-ttu-id="9ad8a-274">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-274">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="9ad8a-275">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-275">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="9ad8a-276">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when users sign in.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-276">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when users sign in.</span></span>

   <span data-ttu-id="9ad8a-277">To add an attribute:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-277">To add an attribute:</span></span>

   <span data-ttu-id="9ad8a-278">1.click **Add attribute**.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-278">1.click **Add attribute**.</span></span> <span data-ttu-id="9ad8a-279">Enter the **Name** and the select the **Value** from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-279">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   <span data-ttu-id="9ad8a-280">2 Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-280">2 Click **Save.**</span></span> <span data-ttu-id="9ad8a-281">You see the new attribute in the table.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-281">You see the new attribute in the table.</span></span>

### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="9ad8a-282">Download the Azure AD metadata or certificate</span><span class="sxs-lookup"><span data-stu-id="9ad8a-282">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="9ad8a-283">To download the application metadata or certificate from Azure AD, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-283">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="9ad8a-284">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-284">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9ad8a-285">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-285">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="9ad8a-286">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-286">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ad8a-287">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-287">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="9ad8a-288">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-288">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="9ad8a-289">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-289">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9ad8a-290">Select the application you have configured single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-290">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="9ad8a-291">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-291">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="9ad8a-292">Go to **SAML Signing Certificate** section, then click **Download** column value.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-292">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="9ad8a-293">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-293">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="9ad8a-294">Azure AD doesn’t provide a URL to get the metadata.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-294">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="9ad8a-295">The metadata can only be retrieved as an XML file.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-295">The metadata can only be retrieved as an XML file.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="9ad8a-296">How to configure password single sign-on for an Azure AD gallery application</span><span class="sxs-lookup"><span data-stu-id="9ad8a-296">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="9ad8a-297">To configure an application from the Azure AD gallery you need to:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-297">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="9ad8a-298">Add an application from the Azure AD gallery</span><span class="sxs-lookup"><span data-stu-id="9ad8a-298">Add an application from the Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="9ad8a-299">Configure the application for password single sign-on</span><span class="sxs-lookup"><span data-stu-id="9ad8a-299">Configure the application for password single sign-on</span></span>](#configure-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="9ad8a-300">Add an application from the Azure AD gallery</span><span class="sxs-lookup"><span data-stu-id="9ad8a-300">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="9ad8a-301">To add an application from the Azure AD Gallery, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-301">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="9ad8a-302">Open the [Azure portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-302">Open the [Azure portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="9ad8a-303">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-303">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="9ad8a-304">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-304">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ad8a-305">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-305">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="9ad8a-306">click the **Add** button at the top-right corner on the **Enterprise Applications** pane.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-306">click the **Add** button at the top-right corner on the **Enterprise Applications** pane.</span></span>

6.  <span data-ttu-id="9ad8a-307">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application</span><span class="sxs-lookup"><span data-stu-id="9ad8a-307">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application</span></span>

7.  <span data-ttu-id="9ad8a-308">Select the application you want to configure for single sign-on</span><span class="sxs-lookup"><span data-stu-id="9ad8a-308">Select the application you want to configure for single sign-on</span></span>

8.  <span data-ttu-id="9ad8a-309">Before adding the application, you can change its name from the **Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-309">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="9ad8a-310">Click **Add** button, to add the application.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-310">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="9ad8a-311">After a short period, you can see the application’s configuration pane.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-311">After a short period, you can see the application’s configuration pane.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="9ad8a-312">Configure the application for password single sign-on</span><span class="sxs-lookup"><span data-stu-id="9ad8a-312">Configure the application for password single sign-on</span></span>

<span data-ttu-id="9ad8a-313">To configure single sign-on for an application, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-313">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="9ad8a-314">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-314">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9ad8a-315">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-315">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="9ad8a-316">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-316">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ad8a-317">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-317">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="9ad8a-318">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-318">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="9ad8a-319">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-319">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9ad8a-320">Select the application you want to configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="9ad8a-320">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="9ad8a-321">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-321">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="9ad8a-322">Select the mode **Password-based Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-322">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="9ad8a-323">Assign users to the application.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-323">Assign users to the application.</span></span>

10. <span data-ttu-id="9ad8a-324">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-324">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="9ad8a-325">Otherwise, users be prompted to enter the credentials themselves upon launch.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-325">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="9ad8a-326">How to configure password single sign-on for a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="9ad8a-326">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="9ad8a-327">To configure an application from the Azure AD gallery you need to:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-327">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="9ad8a-328">Add a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="9ad8a-328">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="9ad8a-329">Configure the application for password single sign-on</span><span class="sxs-lookup"><span data-stu-id="9ad8a-329">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="9ad8a-330">Add a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="9ad8a-330">Add a non-gallery application</span></span>

<span data-ttu-id="9ad8a-331">To add an application from the Azure AD Gallery, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-331">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="9ad8a-332">Open the [Azure portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-332">Open the [Azure portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="9ad8a-333">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-333">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="9ad8a-334">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-334">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ad8a-335">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-335">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="9ad8a-336">click the **Add** button at the top-right corner on the **Enterprise Applications** pane.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-336">click the **Add** button at the top-right corner on the **Enterprise Applications** pane.</span></span>

6.  <span data-ttu-id="9ad8a-337">click **Non-gallery application.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-337">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="9ad8a-338">Enter the name of your application in the **Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-338">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="9ad8a-339">Select **Add.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-339">Select **Add.**</span></span>

<span data-ttu-id="9ad8a-340">After a short period, you be able to see the application’s configuration pane.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-340">After a short period, you be able to see the application’s configuration pane.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="9ad8a-341">Configure the application for password single sign-on</span><span class="sxs-lookup"><span data-stu-id="9ad8a-341">Configure the application for password single sign-on</span></span>

<span data-ttu-id="9ad8a-342">To configure single sign-on for an application, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-342">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="9ad8a-343">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-343">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9ad8a-344">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-344">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="9ad8a-345">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-345">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ad8a-346">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-346">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="9ad8a-347">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-347">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="9ad8a-348">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-348">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9ad8a-349">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-349">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="9ad8a-350">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-350">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="9ad8a-351">Select the mode **Password-based Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-351">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="9ad8a-352">Enter the **Sign-on URL**.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-352">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="9ad8a-353">This is the URL where users enter their username and password to sign in.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-353">This is the URL where users enter their username and password to sign in.</span></span> <span data-ttu-id="9ad8a-354">Ensure the sign-in fields are visible at the URL.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-354">Ensure the sign-in fields are visible at the URL.</span></span>

10. <span data-ttu-id="9ad8a-355">Assign users to the application.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-355">Assign users to the application.</span></span>

11. <span data-ttu-id="9ad8a-356">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-356">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="9ad8a-357">Otherwise, users be prompted to enter the credentials themselves upon launch.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-357">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="9ad8a-358">How to assign a user to an application directly</span><span class="sxs-lookup"><span data-stu-id="9ad8a-358">How to assign a user to an application directly</span></span>

<span data-ttu-id="9ad8a-359">To assign one or more users to an application directly, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-359">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="9ad8a-360">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-360">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9ad8a-361">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-361">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="9ad8a-362">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-362">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9ad8a-363">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-363">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="9ad8a-364">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-364">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9ad8a-365">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="9ad8a-365">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9ad8a-366">Select the application you want to assign a user to from the list.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-366">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="9ad8a-367">Once the application loads, click **Users and Groups** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-367">Once the application loads, click **Users and Groups** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="9ad8a-368">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** pane.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-368">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** pane.</span></span>

9.  <span data-ttu-id="9ad8a-369">click the **Users and groups** selector from the **Add Assignment** pane.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-369">click the **Users and groups** selector from the **Add Assignment** pane.</span></span>

10. <span data-ttu-id="9ad8a-370">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-370">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="9ad8a-371">Hover over the **user** in the list to reveal a **checkbox**.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-371">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="9ad8a-372">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-372">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="9ad8a-373">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-373">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="9ad8a-374">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-374">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="9ad8a-375">**Optional:** click the **Select Role** selector in the **Add Assignment** pane to select a role to assign to the users you have selected.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-375">**Optional:** click the **Select Role** selector in the **Add Assignment** pane to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="9ad8a-376">Click the **Assign** button to assign the application to the selected users.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-376">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="9ad8a-377">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9ad8a-377">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="9ad8a-378">If these troubleshooting steps do not the resolve the issue</span><span class="sxs-lookup"><span data-stu-id="9ad8a-378">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="9ad8a-379">open a support ticket with the following information if available:</span><span class="sxs-lookup"><span data-stu-id="9ad8a-379">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="9ad8a-380">Correlation error ID</span><span class="sxs-lookup"><span data-stu-id="9ad8a-380">Correlation error ID</span></span>

-   <span data-ttu-id="9ad8a-381">UPN (user email address)</span><span class="sxs-lookup"><span data-stu-id="9ad8a-381">UPN (user email address)</span></span>

-   <span data-ttu-id="9ad8a-382">TenantID</span><span class="sxs-lookup"><span data-stu-id="9ad8a-382">TenantID</span></span>

-   <span data-ttu-id="9ad8a-383">Browser type</span><span class="sxs-lookup"><span data-stu-id="9ad8a-383">Browser type</span></span>

-   <span data-ttu-id="9ad8a-384">Time zone and time/timeframe during error occurs</span><span class="sxs-lookup"><span data-stu-id="9ad8a-384">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="9ad8a-385">Fiddler traces</span><span class="sxs-lookup"><span data-stu-id="9ad8a-385">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ad8a-386">Next steps</span><span class="sxs-lookup"><span data-stu-id="9ad8a-386">Next steps</span></span>
[<span data-ttu-id="9ad8a-387">Provide single sign-on to your apps with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="9ad8a-387">Provide single sign-on to your apps with Application Proxy</span></span>](application-proxy-configure-single-sign-on-with-kcd.md)

