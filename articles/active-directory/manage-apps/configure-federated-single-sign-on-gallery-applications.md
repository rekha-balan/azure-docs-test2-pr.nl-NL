---
title: How to configure federated single sign-on for an Azure AD Gallery application | Microsoft Docs
description: How to configure federated single sign-on for an existing Azure AD Gallery application and use tutorials to get going quickly
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
ms.openlocfilehash: a4a80132b243cdf00cac4b14ecb1af3a13864cb5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968839"
---
# <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="a6614-103">How to configure federated single sign-on for an Azure AD Gallery application</span><span class="sxs-lookup"><span data-stu-id="a6614-103">How to configure federated single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="a6614-104">All applications in the Azure AD gallery enabled with Enterprise single sign-on capability has a step-by-step tutorial available.</span><span class="sxs-lookup"><span data-stu-id="a6614-104">All applications in the Azure AD gallery enabled with Enterprise single sign-on capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="a6614-105">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for detailed step-by-step guidance.</span><span class="sxs-lookup"><span data-stu-id="a6614-105">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for detailed step-by-step guidance.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="a6614-106">Overview of steps required</span><span class="sxs-lookup"><span data-stu-id="a6614-106">Overview of steps required</span></span>
<span data-ttu-id="a6614-107">To configure an application from the Azure AD gallery you need to:</span><span class="sxs-lookup"><span data-stu-id="a6614-107">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="a6614-108">Add an application from the Azure AD gallery</span><span class="sxs-lookup"><span data-stu-id="a6614-108">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="a6614-109">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span><span class="sxs-lookup"><span data-stu-id="a6614-109">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="a6614-110">Select User Identifier and add user attributes to be sent to the application</span><span class="sxs-lookup"><span data-stu-id="a6614-110">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="a6614-111">Retrieve Azure AD metadata and certificate</span><span class="sxs-lookup"><span data-stu-id="a6614-111">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="a6614-112">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span><span class="sxs-lookup"><span data-stu-id="a6614-112">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="a6614-113">Assign users to the application</span><span class="sxs-lookup"><span data-stu-id="a6614-113">Assign users to the application</span></span>](#assign-users-to-the-application)

## <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="a6614-114">Add an application from the Azure AD gallery</span><span class="sxs-lookup"><span data-stu-id="a6614-114">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="a6614-115">To add an application from the Azure AD Gallery, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="a6614-115">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="a6614-116">Open the [Azure portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span><span class="sxs-lookup"><span data-stu-id="a6614-116">Open the [Azure portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="a6614-117">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a6614-117">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="a6614-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a6614-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a6614-119">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a6614-119">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="a6614-120">click the **Add** button at the top-right corner on the **Enterprise Applications** pane.</span><span class="sxs-lookup"><span data-stu-id="a6614-120">click the **Add** button at the top-right corner on the **Enterprise Applications** pane.</span></span>

6.  <span data-ttu-id="a6614-121">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span><span class="sxs-lookup"><span data-stu-id="a6614-121">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="a6614-122">Select the application you want to configure for single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a6614-122">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="a6614-123">Before adding the application, you can change its name from the **Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="a6614-123">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="a6614-124">Click **Add** button, to add the application.</span><span class="sxs-lookup"><span data-stu-id="a6614-124">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="a6614-125">After a short period of time, you be able to see the application’s configuration pane.</span><span class="sxs-lookup"><span data-stu-id="a6614-125">After a short period of time, you be able to see the application’s configuration pane.</span></span>

## <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="a6614-126">Configure single sign-on for an application from the Azure AD gallery</span><span class="sxs-lookup"><span data-stu-id="a6614-126">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="a6614-127">To configure single sign-on for an application, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="a6614-127">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="a6614-128">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin**.</span><span class="sxs-lookup"><span data-stu-id="a6614-128">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="a6614-129">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a6614-129">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="a6614-130">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a6614-130">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a6614-131">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a6614-131">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="a6614-132">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="a6614-132">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="a6614-133">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="a6614-133">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a6614-134">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a6614-134">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="a6614-135">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a6614-135">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="a6614-136">Select **SAML-based Sign-on** from the **Mode** dropdown.</span><span class="sxs-lookup"><span data-stu-id="a6614-136">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="a6614-137">Enter the required values in **Domain and URLs.**</span><span class="sxs-lookup"><span data-stu-id="a6614-137">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="a6614-138">You should get these values from the application vendor.</span><span class="sxs-lookup"><span data-stu-id="a6614-138">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="a6614-139">To configure the application as SP-initiated SSO, the Sign-on URL it’s a required value.</span><span class="sxs-lookup"><span data-stu-id="a6614-139">To configure the application as SP-initiated SSO, the Sign-on URL it’s a required value.</span></span> <span data-ttu-id="a6614-140">For some applications, the Identifier is also a required value.</span><span class="sxs-lookup"><span data-stu-id="a6614-140">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="a6614-141">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span><span class="sxs-lookup"><span data-stu-id="a6614-141">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="a6614-142">For some applications, the Identifier is also a required value.</span><span class="sxs-lookup"><span data-stu-id="a6614-142">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="a6614-143">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span><span class="sxs-lookup"><span data-stu-id="a6614-143">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="a6614-144">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span><span class="sxs-lookup"><span data-stu-id="a6614-144">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="a6614-145">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when users sign in.</span><span class="sxs-lookup"><span data-stu-id="a6614-145">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when users sign in.</span></span>

  <span data-ttu-id="a6614-146">To add an attribute:</span><span class="sxs-lookup"><span data-stu-id="a6614-146">To add an attribute:</span></span>
   
   1. <span data-ttu-id="a6614-147">click **Add attribute**.</span><span class="sxs-lookup"><span data-stu-id="a6614-147">click **Add attribute**.</span></span> <span data-ttu-id="a6614-148">Enter the **Name** and the select the **Value** from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="a6614-148">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   1. <span data-ttu-id="a6614-149">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="a6614-149">Click **Save.**</span></span> <span data-ttu-id="a6614-150">You see the new attribute in the table.</span><span class="sxs-lookup"><span data-stu-id="a6614-150">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="a6614-151">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span><span class="sxs-lookup"><span data-stu-id="a6614-151">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="a6614-152">Also, you have the metadata URLs and certificate required to setup SSO with the application.</span><span class="sxs-lookup"><span data-stu-id="a6614-152">Also, you have the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="a6614-153">Click **Save** to save the configuration.</span><span class="sxs-lookup"><span data-stu-id="a6614-153">Click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="a6614-154">Assign users to the application.</span><span class="sxs-lookup"><span data-stu-id="a6614-154">Assign users to the application.</span></span>

## <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="a6614-155">Select User Identifier and add user attributes to be sent to the application</span><span class="sxs-lookup"><span data-stu-id="a6614-155">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="a6614-156">To select the User Identifier or add user attributes, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="a6614-156">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="a6614-157">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="a6614-157">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a6614-158">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a6614-158">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="a6614-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a6614-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a6614-160">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a6614-160">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="a6614-161">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="a6614-161">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="a6614-162">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="a6614-162">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a6614-163">Select the application you have configured single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a6614-163">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="a6614-164">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a6614-164">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="a6614-165">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span><span class="sxs-lookup"><span data-stu-id="a6614-165">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="a6614-166">The selected option needs to match the expected value in the application to authenticate the user.</span><span class="sxs-lookup"><span data-stu-id="a6614-166">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

  >[!NOTE] 
  ><span data-ttu-id="a6614-167">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="a6614-167">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="a6614-168">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="a6614-168">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
  >
  >

9.  <span data-ttu-id="a6614-169">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when users sign in.</span><span class="sxs-lookup"><span data-stu-id="a6614-169">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when users sign in.</span></span>

   <span data-ttu-id="a6614-170">To add an attribute:</span><span class="sxs-lookup"><span data-stu-id="a6614-170">To add an attribute:</span></span>
  
   1. <span data-ttu-id="a6614-171">click **Add attribute**.</span><span class="sxs-lookup"><span data-stu-id="a6614-171">click **Add attribute**.</span></span> <span data-ttu-id="a6614-172">Enter the **Name** and the select the **Value** from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="a6614-172">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="a6614-173">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a6614-173">Click **Save**.</span></span> <span data-ttu-id="a6614-174">You see the new attribute in the table.</span><span class="sxs-lookup"><span data-stu-id="a6614-174">You see the new attribute in the table.</span></span>

## <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="a6614-175">Download the Azure AD metadata or certificate</span><span class="sxs-lookup"><span data-stu-id="a6614-175">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="a6614-176">To download the application metadata or certificate from Azure AD, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="a6614-176">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="a6614-177">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="a6614-177">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a6614-178">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a6614-178">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="a6614-179">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a6614-179">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a6614-180">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a6614-180">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="a6614-181">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="a6614-181">click **All Applications** to view a list of all your applications.</span></span>

  *  <span data-ttu-id="a6614-182">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications**.</span><span class="sxs-lookup"><span data-stu-id="a6614-182">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications**.</span></span>

6.  <span data-ttu-id="a6614-183">Select the application you have configured single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a6614-183">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="a6614-184">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a6614-184">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="a6614-185">Go to **SAML Signing Certificate** section, then click **Download** column value.</span><span class="sxs-lookup"><span data-stu-id="a6614-185">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="a6614-186">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span><span class="sxs-lookup"><span data-stu-id="a6614-186">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

<span data-ttu-id="a6614-187">Azure AD also provides a URL to get the metadata.</span><span class="sxs-lookup"><span data-stu-id="a6614-187">Azure AD also provides a URL to get the metadata.</span></span> <span data-ttu-id="a6614-188">Follow this pattern to get the metadata URL specific to the application: `https://login.microsoftonline.com/<Directory ID>/federationmetadata/2007-06/federationmetadata.xml?appid=<Application ID>`.</span><span class="sxs-lookup"><span data-stu-id="a6614-188">Follow this pattern to get the metadata URL specific to the application: `https://login.microsoftonline.com/<Directory ID>/federationmetadata/2007-06/federationmetadata.xml?appid=<Application ID>`.</span></span>

## <a name="assign-users-to-the-application"></a><span data-ttu-id="a6614-189">Assign users to the application</span><span class="sxs-lookup"><span data-stu-id="a6614-189">Assign users to the application</span></span>

<span data-ttu-id="a6614-190">To assign one or more users to an application directly, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="a6614-190">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="a6614-191">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="a6614-191">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a6614-192">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a6614-192">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="a6614-193">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a6614-193">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a6614-194">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a6614-194">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="a6614-195">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="a6614-195">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="a6614-196">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="a6614-196">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a6614-197">Select the application you want to assign a user to from the list.</span><span class="sxs-lookup"><span data-stu-id="a6614-197">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="a6614-198">Once the application loads, click **Users and Groups** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a6614-198">Once the application loads, click **Users and Groups** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="a6614-199">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** pane.</span><span class="sxs-lookup"><span data-stu-id="a6614-199">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** pane.</span></span>

9.  <span data-ttu-id="a6614-200">click the **Users and groups** selector from the **Add Assignment** pane.</span><span class="sxs-lookup"><span data-stu-id="a6614-200">click the **Users and groups** selector from the **Add Assignment** pane.</span></span>

10. <span data-ttu-id="a6614-201">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span><span class="sxs-lookup"><span data-stu-id="a6614-201">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="a6614-202">Hover over the **user** in the list to reveal a **checkbox**.</span><span class="sxs-lookup"><span data-stu-id="a6614-202">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="a6614-203">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="a6614-203">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="a6614-204">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="a6614-204">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="a6614-205">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="a6614-205">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="a6614-206">**Optional:** click the **Select Role** selector in the **Add Assignment** pane to select a role to assign to the users you have selected.</span><span class="sxs-lookup"><span data-stu-id="a6614-206">**Optional:** click the **Select Role** selector in the **Add Assignment** pane to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="a6614-207">Click the **Assign** button to assign the application to the selected users.</span><span class="sxs-lookup"><span data-stu-id="a6614-207">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="a6614-208">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span><span class="sxs-lookup"><span data-stu-id="a6614-208">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="a6614-209">Customizing the SAML claims sent to an application</span><span class="sxs-lookup"><span data-stu-id="a6614-209">Customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="a6614-210">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span><span class="sxs-lookup"><span data-stu-id="a6614-210">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6614-211">Next steps</span><span class="sxs-lookup"><span data-stu-id="a6614-211">Next steps</span></span>
[<span data-ttu-id="a6614-212">Provide single sign-on to your apps with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="a6614-212">Provide single sign-on to your apps with Application Proxy</span></span>](application-proxy-configure-single-sign-on-with-kcd.md)



