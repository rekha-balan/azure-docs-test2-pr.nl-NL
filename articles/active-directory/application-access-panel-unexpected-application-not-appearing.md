---
title: An assigned application is not appearing on the access panel | Microsoft Docs
description: Troubleshoot why an application is not appearing in the Access Panel
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
ms.openlocfilehash: 605e68dd86e5188f8a872745164ac879c40a1278
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549808"
---
# <a name="an-assigned-application-is-not-appearing-on-the-access-panel"></a><span data-ttu-id="9c6b4-103">An assigned application is not appearing on the access panel</span><span class="sxs-lookup"><span data-stu-id="9c6b4-103">An assigned application is not appearing on the access panel</span></span>

<span data-ttu-id="9c6b4-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="9c6b4-105">These applications are configured on behalf of the user in the Azure AD portal.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="9c6b4-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="9c6b4-107">The type of apps a user may be seeing fall in the following categories:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-107">The type of apps a user may be seeing fall in the following categories:</span></span>

-   <span data-ttu-id="9c6b4-108">Office 365 Applications</span><span class="sxs-lookup"><span data-stu-id="9c6b4-108">Office 365 Applications</span></span>

-   <span data-ttu-id="9c6b4-109">Microsoft and third-party applications configured with federation-based SSO</span><span class="sxs-lookup"><span data-stu-id="9c6b4-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="9c6b4-110">Password-based SSO applications</span><span class="sxs-lookup"><span data-stu-id="9c6b4-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="9c6b4-111">Applications with existing SSO solutions</span><span class="sxs-lookup"><span data-stu-id="9c6b4-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="9c6b4-112">General issues to check first</span><span class="sxs-lookup"><span data-stu-id="9c6b4-112">General issues to check first</span></span>

-   <span data-ttu-id="9c6b4-113">If an application was just added to a user, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is added.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-113">If an application was just added to a user, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is added.</span></span>

-   <span data-ttu-id="9c6b4-114">If a license was just removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-114">If a license was just removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span></span> <span data-ttu-id="9c6b4-115">allow for extra time before signing into the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-115">allow for extra time before signing into the Access Panel.</span></span>

## <a name="problems-related-to-application-configuration"></a><span data-ttu-id="9c6b4-116">Problems related to application configuration</span><span class="sxs-lookup"><span data-stu-id="9c6b4-116">Problems related to application configuration</span></span>

<span data-ttu-id="9c6b4-117">An application may not be appearing in a user’s Access Panel because it is not configured properly.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-117">An application may not be appearing in a user’s Access Panel because it is not configured properly.</span></span> <span data-ttu-id="9c6b4-118">Below are some ways you can troubleshoot issues related to application configuration:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-118">Below are some ways you can troubleshoot issues related to application configuration:</span></span>

-   [<span data-ttu-id="9c6b4-119">How to configure federated single sign-on for an Azure AD gallery application</span><span class="sxs-lookup"><span data-stu-id="9c6b4-119">How to configure federated single sign-on for an Azure AD gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application)

-   [<span data-ttu-id="9c6b4-120">How to configure federated single sign-on for a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="9c6b4-120">How to configure federated single sign-on for a non-gallery application</span></span>](#how-to-configure-federated-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="9c6b4-121">How to configure a password single sign-on application for an Azure AD gallery application</span><span class="sxs-lookup"><span data-stu-id="9c6b4-121">How to configure a password single sign-on application for an Azure AD gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

-   [<span data-ttu-id="9c6b4-122">How to configure a password single sign-on application for a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="9c6b4-122">How to configure a password single sign-on application for a non-gallery application</span></span>](#how-to-configure-password-single-sign-on-for-a-non-gallery-application)

### <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="9c6b4-123">How to configure federated single sign-on for an Azure AD gallery application</span><span class="sxs-lookup"><span data-stu-id="9c6b4-123">How to configure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="9c6b4-124">All application in the Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-124">All application in the Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="9c6b4-125">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-125">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="9c6b4-126">To configure an application from the Azure AD gallery you need to:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-126">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="9c6b4-127">Add an application from the Azure AD gallery</span><span class="sxs-lookup"><span data-stu-id="9c6b4-127">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="9c6b4-128">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span><span class="sxs-lookup"><span data-stu-id="9c6b4-128">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="9c6b4-129">Select User Identifier and add user attributes to be sent to the application</span><span class="sxs-lookup"><span data-stu-id="9c6b4-129">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="9c6b4-130">Retrieve Azure AD metadata and certificate</span><span class="sxs-lookup"><span data-stu-id="9c6b4-130">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="9c6b4-131">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span><span class="sxs-lookup"><span data-stu-id="9c6b4-131">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

#### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="9c6b4-132">Add an application from the Azure AD gallery</span><span class="sxs-lookup"><span data-stu-id="9c6b4-132">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="9c6b4-133">To add an application from the Azure AD Gallery, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-133">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="9c6b4-134">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-134">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="9c6b4-135">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-135">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c6b4-136">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-136">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c6b4-137">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-137">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c6b4-138">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-138">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="9c6b4-139">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-139">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="9c6b4-140">Select the application you want to configure for single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-140">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="9c6b4-141">Before adding the application, you can change its name from the **Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-141">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="9c6b4-142">Click **Add** button, to add the application.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-142">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="9c6b4-143">After a short period, you be able to see the application’s configuration blade.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-143">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="9c6b4-144">Configure single sign-on for an application from the Azure AD gallery</span><span class="sxs-lookup"><span data-stu-id="9c6b4-144">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="9c6b4-145">To configure single sign-on for an application, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-145">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="9c6b4-146">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-146">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9c6b4-147">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-147">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c6b4-148">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-148">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c6b4-149">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-149">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c6b4-150">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-150">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9c6b4-151">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-151">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9c6b4-152">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-152">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="9c6b4-153">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-153">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9c6b4-154">Select **SAML-based Sign-on** from the **Mode** dropdown.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-154">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="9c6b4-155">Enter the required values in **Domain and URLs.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-155">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="9c6b4-156">You should get these values from the application vendor.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-156">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="9c6b4-157">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-157">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="9c6b4-158">For some applications, the Identifier is also a required value.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-158">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="9c6b4-159">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-159">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="9c6b4-160">For some applications, the Identifier is also a required value.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-160">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="9c6b4-161">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-161">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="9c6b4-162">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-162">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="9c6b4-163">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-163">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="9c6b4-164">To add an attribute:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-164">To add an attribute:</span></span>

   1. <span data-ttu-id="9c6b4-165">click **Add attribute**.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-165">click **Add attribute**.</span></span> <span data-ttu-id="9c6b4-166">Enter the **Name** and the select the **Value** from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-166">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="9c6b4-167">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-167">Click **Save.**</span></span> <span data-ttu-id="9c6b4-168">You see the new attribute in the table.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-168">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="9c6b4-169">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-169">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="9c6b4-170">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-170">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="9c6b4-171">Click **Save** to save the configuration.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-171">Click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="9c6b4-172">Assign users to the application.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-172">Assign users to the application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="9c6b4-173">Select User Identifier and add user attributes to be sent to the application</span><span class="sxs-lookup"><span data-stu-id="9c6b4-173">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="9c6b4-174">To select the User Identifier or add user attributes, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-174">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="9c6b4-175">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-175">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9c6b4-176">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-176">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c6b4-177">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-177">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c6b4-178">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-178">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c6b4-179">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-179">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9c6b4-180">If you do not see the application you want to show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-180">If you do not see the application you want to show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9c6b4-181">Select the application you have configured single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-181">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="9c6b4-182">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-182">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9c6b4-183">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-183">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="9c6b4-184">The selected option needs to match the expected value in the application to authenticate the user.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-184">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="9c6b4-185">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-185">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="9c6b4-186">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-186">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="9c6b4-187">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-187">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="9c6b4-188">To add an attribute:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-188">To add an attribute:</span></span>

   1. <span data-ttu-id="9c6b4-189">click **Add attribute**.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-189">click **Add attribute**.</span></span> <span data-ttu-id="9c6b4-190">Enter the **Name** and the select the **Value** from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-190">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="9c6b4-191">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-191">Click **Save.**</span></span> <span data-ttu-id="9c6b4-192">You see the new attribute in the table.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-192">You see the new attribute in the table.</span></span>

#### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="9c6b4-193">Download the Azure AD metadata or certificate</span><span class="sxs-lookup"><span data-stu-id="9c6b4-193">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="9c6b4-194">To download the application metadata or certificate from Azure AD, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-194">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="9c6b4-195">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-195">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9c6b4-196">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-196">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c6b4-197">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-197">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c6b4-198">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-198">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c6b4-199">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-199">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9c6b4-200">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-200">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9c6b4-201">Select the application you have configured single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-201">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="9c6b4-202">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-202">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9c6b4-203">Go to **SAML Signing Certificate** section, then click **Download** column value.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-203">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="9c6b4-204">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-204">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="9c6b4-205">Azure AD doesn’t provide a URL to get the metadata.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-205">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="9c6b4-206">The metadata can only be retrieved as a XML file.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-206">The metadata can only be retrieved as a XML file.</span></span>

### <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="9c6b4-207">How to configure federated single sign-on for a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="9c6b4-207">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="9c6b4-208">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-208">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="9c6b4-209">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="9c6b4-209">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="9c6b4-210">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span><span class="sxs-lookup"><span data-stu-id="9c6b4-210">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="9c6b4-211">Select User Identifier and add user attributes to be sent to the application</span><span class="sxs-lookup"><span data-stu-id="9c6b4-211">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="9c6b4-212">Retrieve Azure AD metadata and certificate</span><span class="sxs-lookup"><span data-stu-id="9c6b4-212">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="9c6b4-213">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span><span class="sxs-lookup"><span data-stu-id="9c6b4-213">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

#### <a name="configure-the-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="9c6b4-214">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span><span class="sxs-lookup"><span data-stu-id="9c6b4-214">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="9c6b4-215">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-215">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="9c6b4-216">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-216">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9c6b4-217">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-217">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c6b4-218">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-218">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c6b4-219">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-219">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c6b4-220">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-220">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="9c6b4-221">click **Non-gallery application** in the **Add your own app** section.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-221">click **Non-gallery application** in the **Add your own app** section.</span></span>

7.  <span data-ttu-id="9c6b4-222">Enter the name of the application in the **Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-222">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="9c6b4-223">Click **Add** button, to add the application.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-223">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="9c6b4-224">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-224">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="9c6b4-225">Select **SAML-based Sign-on** in the **Mode** dropdown.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-225">Select **SAML-based Sign-on** in the **Mode** dropdown.</span></span>

11. <span data-ttu-id="9c6b4-226">Enter the required values in **Domain and URLs.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-226">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="9c6b4-227">You should get these values from the application vendor.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-227">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="9c6b4-228">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-228">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

   2.  <span data-ttu-id="9c6b4-229">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-229">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="9c6b4-230">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-230">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="9c6b4-231">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-231">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="9c6b4-232">To add an attribute:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-232">To add an attribute:</span></span>

   1. <span data-ttu-id="9c6b4-233">click **Add attribute**.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-233">click **Add attribute**.</span></span> <span data-ttu-id="9c6b4-234">Enter the **Name** and the select the **Value** from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-234">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="9c6b4-235">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-235">Click **Save.**</span></span> <span data-ttu-id="9c6b4-236">You see the new attribute in the table.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-236">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="9c6b4-237">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-237">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="9c6b4-238">Also, you has Azure AD URLs and certificate required for the application.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-238">Also, you has Azure AD URLs and certificate required for the application.</span></span>

#### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="9c6b4-239">Select User Identifier and add user attributes to be sent to the application</span><span class="sxs-lookup"><span data-stu-id="9c6b4-239">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="9c6b4-240">To select the User Identifier or add user attributes, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-240">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="9c6b4-241">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-241">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9c6b4-242">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-242">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c6b4-243">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-243">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c6b4-244">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-244">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c6b4-245">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-245">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="9c6b4-246">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-246">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9c6b4-247">Select the application you have configured single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-247">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="9c6b4-248">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-248">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9c6b4-249">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-249">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="9c6b4-250">The selected option needs to match the expected value in the application to authenticate the user.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-250">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE] 
   ><span data-ttu-id="9c6b4-251">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-251">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="9c6b4-252">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-252">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="9c6b4-253">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-253">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="9c6b4-254">To add an attribute:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-254">To add an attribute:</span></span>

   1. <span data-ttu-id="9c6b4-255">click **Add attribute**.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-255">click **Add attribute**.</span></span> <span data-ttu-id="9c6b4-256">Enter the **Name** and the select the **Value** from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-256">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="9c6b4-257">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-257">Click **Save.**</span></span> <span data-ttu-id="9c6b4-258">You see the new attribute in the table.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-258">You see the new attribute in the table.</span></span>

#### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="9c6b4-259">Download the Azure AD metadata or certificate</span><span class="sxs-lookup"><span data-stu-id="9c6b4-259">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="9c6b4-260">To download the application metadata or certificate from Azure AD, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-260">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="9c6b4-261">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-261">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9c6b4-262">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-262">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c6b4-263">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-263">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c6b4-264">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-264">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c6b4-265">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-265">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="9c6b4-266">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-266">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9c6b4-267">Select the application you have configured single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-267">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="9c6b4-268">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-268">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9c6b4-269">Go to **SAML Signing Certificate** section, then click **Download** column value.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-269">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="9c6b4-270">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-270">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="9c6b4-271">Azure AD doesn’t provide a URL to get the metadata.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-271">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="9c6b4-272">The metadata can only be retrieved as a XML file.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-272">The metadata can only be retrieved as a XML file.</span></span>

### <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="9c6b4-273">How to configure password single sign-on for an Azure AD gallery application</span><span class="sxs-lookup"><span data-stu-id="9c6b4-273">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="9c6b4-274">To configure an application from the Azure AD gallery you need to:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-274">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="9c6b4-275">Add an application from the Azure AD gallery</span><span class="sxs-lookup"><span data-stu-id="9c6b4-275">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="9c6b4-276">Configure the application for password single sign-on</span><span class="sxs-lookup"><span data-stu-id="9c6b4-276">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="9c6b4-277">Add an application from the Azure AD gallery</span><span class="sxs-lookup"><span data-stu-id="9c6b4-277">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="9c6b4-278">To add an application from the Azure AD Gallery, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-278">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="9c6b4-279">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-279">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="9c6b4-280">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-280">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c6b4-281">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-281">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c6b4-282">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-282">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c6b4-283">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-283">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="9c6b4-284">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-284">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="9c6b4-285">Select the application you want to configure for single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-285">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="9c6b4-286">Before adding the application, you can change its name from the **Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-286">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="9c6b4-287">Click **Add** button, to add the application.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-287">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="9c6b4-288">After a short period, you be able to see the application’s configuration blade.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-288">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="9c6b4-289">Configure the application for password single sign-on</span><span class="sxs-lookup"><span data-stu-id="9c6b4-289">Configure the application for password single sign-on</span></span>

<span data-ttu-id="9c6b4-290">To configure single sign-on for an application, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-290">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="9c6b4-291">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-291">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9c6b4-292">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-292">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c6b4-293">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-293">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c6b4-294">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-294">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c6b4-295">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-295">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="9c6b4-296">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-296">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9c6b4-297">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-297">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="9c6b4-298">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-298">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9c6b4-299">Select the mode **Password-based Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-299">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="9c6b4-300">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="9c6b4-300">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="9c6b4-301">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-301">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="9c6b4-302">Otherwise, users be prompted to enter the credentials themselves upon launch.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-302">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

### <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="9c6b4-303">How to configure password single sign-on for a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="9c6b4-303">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="9c6b4-304">To configure an application from the Azure AD gallery you need to:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-304">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="9c6b4-305">Add a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="9c6b4-305">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="9c6b4-306">Configure the application for password single sign-on</span><span class="sxs-lookup"><span data-stu-id="9c6b4-306">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

#### <a name="add-a-non-gallery-application"></a><span data-ttu-id="9c6b4-307">Add a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="9c6b4-307">Add a non-gallery application</span></span>

<span data-ttu-id="9c6b4-308">To add an application from the Azure AD Gallery, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-308">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="9c6b4-309">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-309">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="9c6b4-310">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-310">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c6b4-311">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-311">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c6b4-312">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-312">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c6b4-313">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-313">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="9c6b4-314">click **Non-gallery application.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-314">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="9c6b4-315">Enter the name of your application in the **Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-315">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="9c6b4-316">Select **Add.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-316">Select **Add.**</span></span>

<span data-ttu-id="9c6b4-317">After a short period, you be able to see the application’s configuration blade.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-317">After a short period, you be able to see the application’s configuration blade.</span></span>

#### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="9c6b4-318">Configure the application for password single sign-on</span><span class="sxs-lookup"><span data-stu-id="9c6b4-318">Configure the application for password single sign-on</span></span>

<span data-ttu-id="9c6b4-319">To configure single sign-on for an application, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-319">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="9c6b4-320">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-320">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9c6b4-321">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-321">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c6b4-322">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-322">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c6b4-323">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-323">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c6b4-324">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-324">click **All Applications** to view a list of all your applications.</span></span>

    1.  <span data-ttu-id="9c6b4-325">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-325">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9c6b4-326">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-326">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="9c6b4-327">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-327">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9c6b4-328">Select the mode **Password-based Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-328">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="9c6b4-329">Enter the **Sign-on URL**.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-329">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="9c6b4-330">This is the URL where users enter their username and password to sign in to.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-330">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="9c6b4-331">Ensure the sign in fields are visible at the URL.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-331">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="9c6b4-332">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="9c6b4-332">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

11. <span data-ttu-id="9c6b4-333">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-333">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="9c6b4-334">Otherwise, users be prompted to enter the credentials themselves upon launch.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-334">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="problems-related-to-assigning-applications-to-users"></a><span data-ttu-id="9c6b4-335">Problems related to assigning applications to users</span><span class="sxs-lookup"><span data-stu-id="9c6b4-335">Problems related to assigning applications to users</span></span>

<span data-ttu-id="9c6b4-336">A user may not be seeing an application on their Access Panel because they are not assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-336">A user may not be seeing an application on their Access Panel because they are not assigned to the application.</span></span> <span data-ttu-id="9c6b4-337">Below are some ways to check:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-337">Below are some ways to check:</span></span>

-   [<span data-ttu-id="9c6b4-338">Check if a user is assigned to the application</span><span class="sxs-lookup"><span data-stu-id="9c6b4-338">Check if a user is assigned to the application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="9c6b4-339">How to assign a user to an application directly</span><span class="sxs-lookup"><span data-stu-id="9c6b4-339">How to assign a user to an application directly</span></span>](#how-to-assign-a-user-to-an-application-directly)

-   [<span data-ttu-id="9c6b4-340">Check if a user is assigned to a license related to the application</span><span class="sxs-lookup"><span data-stu-id="9c6b4-340">Check if a user is assigned to a license related to the application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)

-   [<span data-ttu-id="9c6b4-341">How to assign a license to a user</span><span class="sxs-lookup"><span data-stu-id="9c6b4-341">How to assign a license to a user</span></span>](#how-to-assign-a-user-a-license)

### <a name="check-if-a-user-is-assigned-to-the-application"></a><span data-ttu-id="9c6b4-342">Check if a user is assigned to the application</span><span class="sxs-lookup"><span data-stu-id="9c6b4-342">Check if a user is assigned to the application</span></span>

<span data-ttu-id="9c6b4-343">To check if a user is assigned to the application, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-343">To check if a user is assigned to the application, follow the steps below:</span></span>

1.  <span data-ttu-id="9c6b4-344">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-344">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9c6b4-345">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-345">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c6b4-346">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-346">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c6b4-347">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-347">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c6b4-348">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-348">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="9c6b4-349">**Search** for the name of the application in question.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-349">**Search** for the name of the application in question.</span></span>

7.  <span data-ttu-id="9c6b4-350">click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-350">click **Users and groups**.</span></span>

8.  <span data-ttu-id="9c6b4-351">Check to see if your user is assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-351">Check to see if your user is assigned to the application.</span></span>

   * <span data-ttu-id="9c6b4-352">If not follow the steps in “How to assign a user to an application directly” to do so.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-352">If not follow the steps in “How to assign a user to an application directly” to do so.</span></span>

### <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="9c6b4-353">How to assign a user to an application directly</span><span class="sxs-lookup"><span data-stu-id="9c6b4-353">How to assign a user to an application directly</span></span>

<span data-ttu-id="9c6b4-354">To assign one or more users to an application directly, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-354">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="9c6b4-355">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-355">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="9c6b4-356">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-356">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c6b4-357">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-357">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c6b4-358">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-358">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c6b4-359">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-359">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9c6b4-360">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-360">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9c6b4-361">Select the application you want to assign a user to from the list.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-361">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="9c6b4-362">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-362">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9c6b4-363">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-363">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="9c6b4-364">click the **Users and groups** selector from the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-364">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="9c6b4-365">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-365">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="9c6b4-366">Hover over the **user** in the list to reveal a **checkbox**.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-366">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="9c6b4-367">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-367">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="9c6b4-368">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-368">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="9c6b4-369">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-369">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="9c6b4-370">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-370">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="9c6b4-371">Click the **Assign** button to assign the application to the selected users.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-371">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="9c6b4-372">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-372">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-to-the-application"></a><span data-ttu-id="9c6b4-373">Check if a user is under a license related to the application</span><span class="sxs-lookup"><span data-stu-id="9c6b4-373">Check if a user is under a license related to the application</span></span>

<span data-ttu-id="9c6b4-374">To check a user’s assigned licenses, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-374">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="9c6b4-375">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-375">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9c6b4-376">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-376">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c6b4-377">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-377">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c6b4-378">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-378">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="9c6b4-379">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-379">click **All users**.</span></span>

6.  <span data-ttu-id="9c6b4-380">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-380">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="9c6b4-381">click **Licenses** to see which licenses the user currently has assigned.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-381">click **Licenses** to see which licenses the user currently has assigned.</span></span>

  * <span data-ttu-id="9c6b4-382">If the user is assigned to an Office license this enable First Party Office applications to appear on the user’s Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-382">If the user is assigned to an Office license this enable First Party Office applications to appear on the user’s Access Panel.</span></span>

### <a name="how-to-assign-a-user-a-license"></a><span data-ttu-id="9c6b4-383">How to assign a user a license</span><span class="sxs-lookup"><span data-stu-id="9c6b4-383">How to assign a user a license</span></span> 

<span data-ttu-id="9c6b4-384">To assign a license to a user, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-384">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="9c6b4-385">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-385">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9c6b4-386">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-386">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c6b4-387">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-387">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c6b4-388">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-388">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="9c6b4-389">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-389">click **All users**.</span></span>

6.  <span data-ttu-id="9c6b4-390">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-390">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="9c6b4-391">click **Licenses** to see which licenses the user currently has assigned.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-391">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="9c6b4-392">click the **Assign** button.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-392">click the **Assign** button.</span></span>

9.  <span data-ttu-id="9c6b4-393">Select **one or more products** from the list of available products.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-393">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="9c6b4-394">**Optional** click the **assignment options** item to granularly assign products.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-394">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="9c6b4-395">Click **Ok** when this is completed.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-395">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="9c6b4-396">Click the **Assign** button to assign these licenses to this user.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-396">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="problems-related-to-assigning-applications-to-groups"></a><span data-ttu-id="9c6b4-397">Problems related to assigning applications to groups</span><span class="sxs-lookup"><span data-stu-id="9c6b4-397">Problems related to assigning applications to groups</span></span>

<span data-ttu-id="9c6b4-398">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-398">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span></span> <span data-ttu-id="9c6b4-399">Below are some ways to check:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-399">Below are some ways to check:</span></span>

-   [<span data-ttu-id="9c6b4-400">Check a user’s group memberships</span><span class="sxs-lookup"><span data-stu-id="9c6b4-400">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="9c6b4-401">How to assign an application to a group directly</span><span class="sxs-lookup"><span data-stu-id="9c6b4-401">How to assign an application to a group directly</span></span>](#how-to-assign-an-application-to-a-group-directly)

-   [<span data-ttu-id="9c6b4-402">Check if a user is part of group assigned to a license</span><span class="sxs-lookup"><span data-stu-id="9c6b4-402">Check if a user is part of group assigned to a license</span></span>](#check-if-a-user-is-part-of-group-assigned-to-a-license)

-   [<span data-ttu-id="9c6b4-403">How to assign a license to a group</span><span class="sxs-lookup"><span data-stu-id="9c6b4-403">How to assign a license to a group</span></span>](#how-to-assign-a-license-to-a-group)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="9c6b4-404">Check a user’s group memberships</span><span class="sxs-lookup"><span data-stu-id="9c6b4-404">Check a user’s group memberships</span></span>

<span data-ttu-id="9c6b4-405">To check a group’s membership, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-405">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="9c6b4-406">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-406">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9c6b4-407">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-407">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c6b4-408">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-408">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c6b4-409">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-409">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="9c6b4-410">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-410">click **All users**.</span></span>

6.  <span data-ttu-id="9c6b4-411">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-411">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="9c6b4-412">click **Groups**.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-412">click **Groups**.</span></span>

8.  <span data-ttu-id="9c6b4-413">Check to see if your user is part of a Group assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-413">Check to see if your user is part of a Group assigned to the application.</span></span>

  * <span data-ttu-id="9c6b4-414">If you want to remove the user from the group, **click the row** of the group and select delete.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-414">If you want to remove the user from the group, **click the row** of the group and select delete.</span></span>

### <a name="how-to-assign-an-application-to-a-group-directly"></a><span data-ttu-id="9c6b4-415">How to assign an application to a group directly</span><span class="sxs-lookup"><span data-stu-id="9c6b4-415">How to assign an application to a group directly</span></span>

<span data-ttu-id="9c6b4-416">To assign one or more groups to an application directly, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-416">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="9c6b4-417">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-417">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator**.</span></span>

2.  <span data-ttu-id="9c6b4-418">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-418">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c6b4-419">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-419">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c6b4-420">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-420">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9c6b4-421">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-421">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9c6b4-422">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-422">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9c6b4-423">Select the application you want to assign a user to from the list.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-423">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="9c6b4-424">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-424">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9c6b4-425">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-425">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="9c6b4-426">click the **Users and groups** selector from the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-426">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="9c6b4-427">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-427">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="9c6b4-428">Hover over the **group** in the list to reveal a **checkbox**.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-428">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="9c6b4-429">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-429">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="9c6b4-430">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-430">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="9c6b4-431">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-431">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="9c6b4-432">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-432">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="9c6b4-433">Click the **Assign** button to assign the application to the selected groups.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-433">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="9c6b4-434">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-434">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

### <a name="check-if-a-user-is-part-of-group-assigned-to-a-license"></a><span data-ttu-id="9c6b4-435">Check if a user is part of group assigned to a license</span><span class="sxs-lookup"><span data-stu-id="9c6b4-435">Check if a user is part of group assigned to a license</span></span>

1.  <span data-ttu-id="9c6b4-436">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-436">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9c6b4-437">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-437">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c6b4-438">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-438">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c6b4-439">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-439">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="9c6b4-440">click **All users**.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-440">click **All users**.</span></span>

6.  <span data-ttu-id="9c6b4-441">**Search** for the user you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-441">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="9c6b4-442">click **Groups**.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-442">click **Groups**.</span></span>

8.  <span data-ttu-id="9c6b4-443">click the row of a specific group.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-443">click the row of a specific group.</span></span>

9.  <span data-ttu-id="9c6b4-444">click **Licenses** to see which licenses the group has assigned to it.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-444">click **Licenses** to see which licenses the group has assigned to it.</span></span>

   * <span data-ttu-id="9c6b4-445">If the group is assigned to an Office license this may enable certain First Party Office applications to appear on the user’s Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-445">If the group is assigned to an Office license this may enable certain First Party Office applications to appear on the user’s Access Panel.</span></span>

### <a name="how-to-assign-a-license-to-a-group"></a><span data-ttu-id="9c6b4-446">How to assign a license to a group</span><span class="sxs-lookup"><span data-stu-id="9c6b4-446">How to assign a license to a group</span></span>

<span data-ttu-id="9c6b4-447">To assign a license to a group, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9c6b4-447">To assign a license to a group, follow the steps below:</span></span>

1.  <span data-ttu-id="9c6b4-448">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="9c6b4-448">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9c6b4-449">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-449">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9c6b4-450">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-450">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9c6b4-451">click **Users and groups** in the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-451">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="9c6b4-452">click **All groups**.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-452">click **All groups**.</span></span>

6.  <span data-ttu-id="9c6b4-453">**Search** for the group you are interested in and **click the row** to select.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-453">**Search** for the group you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="9c6b4-454">click **Licenses** to see which licenses the group currently has assigned.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-454">click **Licenses** to see which licenses the group currently has assigned.</span></span>

8.  <span data-ttu-id="9c6b4-455">click the **Assign** button.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-455">click the **Assign** button.</span></span>

9.  <span data-ttu-id="9c6b4-456">Select **one or more products** from the list of available products.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-456">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="9c6b4-457">**Optional** click the **assignment options** item to granularly assign products.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-457">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="9c6b4-458">Click **Ok** when this is completed.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-458">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="9c6b4-459">Click the **Assign** button to assign these licenses to this group.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-459">Click the **Assign** button to assign these licenses to this group.</span></span> <span data-ttu-id="9c6b4-460">This may take a long time, depending on the size and complexity of the group.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-460">This may take a long time, depending on the size and complexity of the group.</span></span>

>[!NOTE]
><span data-ttu-id="9c6b4-461">To do this faster, consider temporarily assigning a license to the user directly.</span><span class="sxs-lookup"><span data-stu-id="9c6b4-461">To do this faster, consider temporarily assigning a license to the user directly.</span></span> 
>
>

## <a name="next-steps"></a><span data-ttu-id="9c6b4-462">Next steps</span><span class="sxs-lookup"><span data-stu-id="9c6b4-462">Next steps</span></span>
[<span data-ttu-id="9c6b4-463">Add new users to Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9c6b4-463">Add new users to Azure Active Directory</span></span>](active-directory-users-create-azure-portal.md)

