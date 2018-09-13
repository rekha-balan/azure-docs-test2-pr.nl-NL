---
title: How to configure federated single sign-on for a non-gallery application | Microsoft Docs
description: How to configure federated single sign-on for a custom non-gallery application that you want to integrate with Azure AD
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
ms.openlocfilehash: cdd867bd3ef448a9d01577abc107150597537da1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564313"
---
# <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="3b25a-103">How to configure federated single sign-on for a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="3b25a-103">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="3b25a-104">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="3b25a-104">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="3b25a-105">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="3b25a-105">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="3b25a-106">Overview of steps required</span><span class="sxs-lookup"><span data-stu-id="3b25a-106">Overview of steps required</span></span>
<span data-ttu-id="3b25a-107">Below is a high level overview of the steps required to configure federated single sign-on for a non-gallery (e.g., custom) application.</span><span class="sxs-lookup"><span data-stu-id="3b25a-107">Below is a high level overview of the steps required to configure federated single sign-on for a non-gallery (e.g., custom) application.</span></span>

-   [<span data-ttu-id="3b25a-108">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span><span class="sxs-lookup"><span data-stu-id="3b25a-108">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="3b25a-109">Select User Identifier and add user attributes to be sent to the application</span><span class="sxs-lookup"><span data-stu-id="3b25a-109">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="3b25a-110">Retrieve Azure AD metadata and certificate</span><span class="sxs-lookup"><span data-stu-id="3b25a-110">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="3b25a-111">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span><span class="sxs-lookup"><span data-stu-id="3b25a-111">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#_Configuring_single_sign-on)

-   [<span data-ttu-id="3b25a-112">Assign users to the application</span><span class="sxs-lookup"><span data-stu-id="3b25a-112">Assign users to the application</span></span>](#_Assign_users_to_the_application)

## <a name="configuring-single-sign-on-to-non-gallery-applications"></a><span data-ttu-id="3b25a-113">Configuring single sign-on to non-gallery applications</span><span class="sxs-lookup"><span data-stu-id="3b25a-113">Configuring single sign-on to non-gallery applications</span></span>

<span data-ttu-id="3b25a-114">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="3b25a-114">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="3b25a-115">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="3b25a-115">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="3b25a-116">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="3b25a-116">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3b25a-117">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="3b25a-117">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3b25a-118">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="3b25a-118">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3b25a-119">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span><span class="sxs-lookup"><span data-stu-id="3b25a-119">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="3b25a-120">click **Non-gallery application** in the **Add your own app** section</span><span class="sxs-lookup"><span data-stu-id="3b25a-120">click **Non-gallery application** in the **Add your own app** section</span></span>

7.  <span data-ttu-id="3b25a-121">Enter the name of the application in the **Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="3b25a-121">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="3b25a-122">Click **Add** button, to add the application.</span><span class="sxs-lookup"><span data-stu-id="3b25a-122">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="3b25a-123">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="3b25a-123">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="3b25a-124">Select **SAML-based Sign-on** in the **Mode** dropdown.</span><span class="sxs-lookup"><span data-stu-id="3b25a-124">Select **SAML-based Sign-on** in the **Mode** dropdown.</span></span>

11. <span data-ttu-id="3b25a-125">Enter the required values in **Domain and URLs.**</span><span class="sxs-lookup"><span data-stu-id="3b25a-125">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="3b25a-126">You should get these values from the application vendor.</span><span class="sxs-lookup"><span data-stu-id="3b25a-126">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="3b25a-127">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span><span class="sxs-lookup"><span data-stu-id="3b25a-127">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

   2. <span data-ttu-id="3b25a-128">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span><span class="sxs-lookup"><span data-stu-id="3b25a-128">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="3b25a-129">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span><span class="sxs-lookup"><span data-stu-id="3b25a-129">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="3b25a-130">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span><span class="sxs-lookup"><span data-stu-id="3b25a-130">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="3b25a-131">To add an attribute:</span><span class="sxs-lookup"><span data-stu-id="3b25a-131">To add an attribute:</span></span>

   1. <span data-ttu-id="3b25a-132">click **Add attribute**.</span><span class="sxs-lookup"><span data-stu-id="3b25a-132">click **Add attribute**.</span></span> <span data-ttu-id="3b25a-133">Enter the **Name** and the select the **Value** from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="3b25a-133">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="3b25a-134">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="3b25a-134">Click **Save.**</span></span> <span data-ttu-id="3b25a-135">You see the new attribute in the table.</span><span class="sxs-lookup"><span data-stu-id="3b25a-135">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="3b25a-136">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span><span class="sxs-lookup"><span data-stu-id="3b25a-136">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="3b25a-137">Also, you has Azure AD URLs and certificate required for the application.</span><span class="sxs-lookup"><span data-stu-id="3b25a-137">Also, you has Azure AD URLs and certificate required for the application.</span></span>

15. [<span data-ttu-id="3b25a-138">Assign users to the application.</span><span class="sxs-lookup"><span data-stu-id="3b25a-138">Assign users to the application.</span></span>](#assign-users-to-the-application)

## <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="3b25a-139">Select User Identifier and add user attributes to be sent to the application</span><span class="sxs-lookup"><span data-stu-id="3b25a-139">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="3b25a-140">To select the User Identifier or add user attributes, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="3b25a-140">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="3b25a-141">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="3b25a-141">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="3b25a-142">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="3b25a-142">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3b25a-143">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="3b25a-143">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3b25a-144">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="3b25a-144">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3b25a-145">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="3b25a-145">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="3b25a-146">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="3b25a-146">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="3b25a-147">Select the application you have configured single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3b25a-147">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="3b25a-148">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="3b25a-148">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3b25a-149">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span><span class="sxs-lookup"><span data-stu-id="3b25a-149">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="3b25a-150">The selected option needs to match the expected value in the application to authenticate the user.</span><span class="sxs-lookup"><span data-stu-id="3b25a-150">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

 ><span data-ttu-id="3b25a-151">[!NOTE} Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="3b25a-151">[!NOTE} Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="3b25a-152">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="3b25a-152">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
 >
 >

9.  <span data-ttu-id="3b25a-153">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span><span class="sxs-lookup"><span data-stu-id="3b25a-153">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="3b25a-154">To add an attribute:</span><span class="sxs-lookup"><span data-stu-id="3b25a-154">To add an attribute:</span></span>

   1. <span data-ttu-id="3b25a-155">click **Add attribute**.</span><span class="sxs-lookup"><span data-stu-id="3b25a-155">click **Add attribute**.</span></span> <span data-ttu-id="3b25a-156">Enter the **Name** and the select the **Value** from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="3b25a-156">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="3b25a-157">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="3b25a-157">Click **Save.**</span></span> <span data-ttu-id="3b25a-158">You see the new attribute in the table.</span><span class="sxs-lookup"><span data-stu-id="3b25a-158">You see the new attribute in the table.</span></span>

## <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="3b25a-159">Download the Azure AD metadata or certificate</span><span class="sxs-lookup"><span data-stu-id="3b25a-159">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="3b25a-160">To download the application metadata or certificate from Azure AD, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="3b25a-160">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="3b25a-161">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="3b25a-161">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="3b25a-162">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="3b25a-162">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3b25a-163">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="3b25a-163">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3b25a-164">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="3b25a-164">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3b25a-165">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="3b25a-165">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="3b25a-166">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="3b25a-166">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="3b25a-167">Select the application you have configured single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3b25a-167">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="3b25a-168">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="3b25a-168">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3b25a-169">Go to **SAML Signing Certificate** section, then click **Download** column value.</span><span class="sxs-lookup"><span data-stu-id="3b25a-169">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="3b25a-170">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span><span class="sxs-lookup"><span data-stu-id="3b25a-170">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="3b25a-171">Azure AD doesn’t provide a URL to get the metadata.</span><span class="sxs-lookup"><span data-stu-id="3b25a-171">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="3b25a-172">The metadata can only be retrieved as a XML file.</span><span class="sxs-lookup"><span data-stu-id="3b25a-172">The metadata can only be retrieved as a XML file.</span></span>

## <a name="assign-users-to-the-application"></a><span data-ttu-id="3b25a-173">Assign users to the application</span><span class="sxs-lookup"><span data-stu-id="3b25a-173">Assign users to the application</span></span>

<span data-ttu-id="3b25a-174">To assign one or more users to an application directly, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="3b25a-174">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="3b25a-175">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="3b25a-175">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3b25a-176">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="3b25a-176">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3b25a-177">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="3b25a-177">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3b25a-178">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="3b25a-178">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3b25a-179">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="3b25a-179">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="3b25a-180">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="3b25a-180">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="3b25a-181">Select the application you want to assign a user to from the list.</span><span class="sxs-lookup"><span data-stu-id="3b25a-181">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="3b25a-182">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="3b25a-182">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3b25a-183">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="3b25a-183">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="3b25a-184">click the **Users and groups** selector from the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="3b25a-184">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="3b25a-185">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span><span class="sxs-lookup"><span data-stu-id="3b25a-185">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="3b25a-186">Hover over the **user** in the list to reveal a **checkbox**.</span><span class="sxs-lookup"><span data-stu-id="3b25a-186">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="3b25a-187">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="3b25a-187">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="3b25a-188">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="3b25a-188">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="3b25a-189">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="3b25a-189">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="3b25a-190">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span><span class="sxs-lookup"><span data-stu-id="3b25a-190">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="3b25a-191">Click the **Assign** button to assign the application to the selected users.</span><span class="sxs-lookup"><span data-stu-id="3b25a-191">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="3b25a-192">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span><span class="sxs-lookup"><span data-stu-id="3b25a-192">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b25a-193">Next steps</span><span class="sxs-lookup"><span data-stu-id="3b25a-193">Next steps</span></span>
[<span data-ttu-id="3b25a-194">Provide single sign-on to your apps with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="3b25a-194">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
