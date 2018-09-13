---
title: Configure single sign-on - Azure Active Directory | Microsoft Docs
description: This tutorial uses the Azure portal to configure SAML-based single sign-on for an application with Azure Active Directory (Azure AD).
services: active-directory
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.topic: tutorial
ms.workload: identity
ms.date: 08/09/2018
ms.author: barbkess
ms.reviewer: arvinh,luleon
ms.openlocfilehash: b0180f162996c5fc4647071feaf02d42320b7c9a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869272"
---
# <a name="tutorial-configure-saml-based-single-sign-on-for-an-application-with-azure-active-directory"></a><span data-ttu-id="622a9-103">Tutorial: Configure SAML-based single sign-on for an application with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="622a9-103">Tutorial: Configure SAML-based single sign-on for an application with Azure Active Directory</span></span>

<span data-ttu-id="622a9-104">This tutorial uses the [Azure portal](https://portal.azure.com) to configure SAML-based single sign-on for an application with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="622a9-104">This tutorial uses the [Azure portal](https://portal.azure.com) to configure SAML-based single sign-on for an application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="622a9-105">Use this tutorial for configuring applications that do not have an [application-specific tutorial](../saas-apps/tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="622a9-105">Use this tutorial for configuring applications that do not have an [application-specific tutorial](../saas-apps/tutorial-list.md).</span></span> 


<span data-ttu-id="622a9-106">This tutorial uses the Azure portal to:</span><span class="sxs-lookup"><span data-stu-id="622a9-106">This tutorial uses the Azure portal to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="622a9-107">Select the SAML-based single sign-on mode</span><span class="sxs-lookup"><span data-stu-id="622a9-107">Select the SAML-based single sign-on mode</span></span>
> * <span data-ttu-id="622a9-108">Configure application-specific domain and URLs</span><span class="sxs-lookup"><span data-stu-id="622a9-108">Configure application-specific domain and URLs</span></span>
> * <span data-ttu-id="622a9-109">Configure user attributes</span><span class="sxs-lookup"><span data-stu-id="622a9-109">Configure user attributes</span></span>
> * <span data-ttu-id="622a9-110">Create a SAML signing certificate</span><span class="sxs-lookup"><span data-stu-id="622a9-110">Create a SAML signing certificate</span></span>
> * <span data-ttu-id="622a9-111">Assign users to the application</span><span class="sxs-lookup"><span data-stu-id="622a9-111">Assign users to the application</span></span>
> * <span data-ttu-id="622a9-112">Configure the application for SAML-based single sign-on</span><span class="sxs-lookup"><span data-stu-id="622a9-112">Configure the application for SAML-based single sign-on</span></span>
> * <span data-ttu-id="622a9-113">Test the SAML settings</span><span class="sxs-lookup"><span data-stu-id="622a9-113">Test the SAML settings</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="622a9-114">Before you begin</span><span class="sxs-lookup"><span data-stu-id="622a9-114">Before you begin</span></span>

1. <span data-ttu-id="622a9-115">If the application has not been added to your Azure AD tenant, see  [Quickstart: Add an application to your Azure AD tenant](add-application-portal.md).</span><span class="sxs-lookup"><span data-stu-id="622a9-115">If the application has not been added to your Azure AD tenant, see  [Quickstart: Add an application to your Azure AD tenant](add-application-portal.md).</span></span>

2. <span data-ttu-id="622a9-116">Ask your application vendor for the information described in [Configure domain and URLS](#configure-domain-and-urls).</span><span class="sxs-lookup"><span data-stu-id="622a9-116">Ask your application vendor for the information described in [Configure domain and URLS](#configure-domain-and-urls).</span></span>

3. <span data-ttu-id="622a9-117">To test the steps in this tutorial, we recommend using a non-production environment.</span><span class="sxs-lookup"><span data-stu-id="622a9-117">To test the steps in this tutorial, we recommend using a non-production environment.</span></span> <span data-ttu-id="622a9-118">If you don't have an Azure AD non-production environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="622a9-118">If you don't have an Azure AD non-production environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

4. <span data-ttu-id="622a9-119">Sign in to the [Azure portal](https://portal.azure.com) as a global admin for your Azure AD tenant, a cloud application admin, or an application admin.</span><span class="sxs-lookup"><span data-stu-id="622a9-119">Sign in to the [Azure portal](https://portal.azure.com) as a global admin for your Azure AD tenant, a cloud application admin, or an application admin.</span></span>

## <a name="select-a-single-sign-on-mode"></a><span data-ttu-id="622a9-120">Select a single sign-on mode</span><span class="sxs-lookup"><span data-stu-id="622a9-120">Select a single sign-on mode</span></span>

<span data-ttu-id="622a9-121">After an application is added to your Azure AD tenant, you are ready to configure single sign-on for the application.</span><span class="sxs-lookup"><span data-stu-id="622a9-121">After an application is added to your Azure AD tenant, you are ready to configure single sign-on for the application.</span></span>

<span data-ttu-id="622a9-122">To open the single sign-on settings:</span><span class="sxs-lookup"><span data-stu-id="622a9-122">To open the single sign-on settings:</span></span>

1. <span data-ttu-id="622a9-123">In the [Azure portal](https://portal.azure.com), on the left navigation panel, click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="622a9-123">In the [Azure portal](https://portal.azure.com), on the left navigation panel, click **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="622a9-124">In the **Azure Active Directory** blade, click **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="622a9-124">In the **Azure Active Directory** blade, click **Enterprise applications**.</span></span> <span data-ttu-id="622a9-125">The **All applications** blade opens to show a random sample of the applications in your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="622a9-125">The **All applications** blade opens to show a random sample of the applications in your Azure AD tenant.</span></span> 

3. <span data-ttu-id="622a9-126">In the **Application Type** menu, select **All applications**, and click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="622a9-126">In the **Application Type** menu, select **All applications**, and click **Apply**.</span></span>

4. <span data-ttu-id="622a9-127">Enter the name of the application for which you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="622a9-127">Enter the name of the application for which you want to configure single sign-on.</span></span> <span data-ttu-id="622a9-128">Choose your own application, or use the GitHub-test application that was added in the [add application](add-application-portal.md) quickstart.</span><span class="sxs-lookup"><span data-stu-id="622a9-128">Choose your own application, or use the GitHub-test application that was added in the [add application](add-application-portal.md) quickstart.</span></span>

5. <span data-ttu-id="622a9-129">Click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="622a9-129">Click **Single sign-on**.</span></span> <span data-ttu-id="622a9-130">Under **Single Sign-on Mode**, **SAML-based Sign-on** appears as the default option.</span><span class="sxs-lookup"><span data-stu-id="622a9-130">Under **Single Sign-on Mode**, **SAML-based Sign-on** appears as the default option.</span></span> 

    ![Configuration options](media/configure-single-sign-on-portal/config-options.png)

6. <span data-ttu-id="622a9-132">Click **Save** at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="622a9-132">Click **Save** at the top of the blade.</span></span> 

## <a name="configure-domain-and-urls"></a><span data-ttu-id="622a9-133">Configure domain and URLs</span><span class="sxs-lookup"><span data-stu-id="622a9-133">Configure domain and URLs</span></span>

<span data-ttu-id="622a9-134">To configure the domain and URLs:</span><span class="sxs-lookup"><span data-stu-id="622a9-134">To configure the domain and URLs:</span></span>

1. <span data-ttu-id="622a9-135">Contact the application vendor to get the correct information for the following settings:</span><span class="sxs-lookup"><span data-stu-id="622a9-135">Contact the application vendor to get the correct information for the following settings:</span></span>

    | <span data-ttu-id="622a9-136">Configuration setting</span><span class="sxs-lookup"><span data-stu-id="622a9-136">Configuration setting</span></span> | <span data-ttu-id="622a9-137">SP-Initiated</span><span class="sxs-lookup"><span data-stu-id="622a9-137">SP-Initiated</span></span> | <span data-ttu-id="622a9-138">idP-Initiated</span><span class="sxs-lookup"><span data-stu-id="622a9-138">idP-Initiated</span></span> | <span data-ttu-id="622a9-139">Description</span><span class="sxs-lookup"><span data-stu-id="622a9-139">Description</span></span> |
    |:--|:--|:--|:--|
    | <span data-ttu-id="622a9-140">Sign-on URL</span><span class="sxs-lookup"><span data-stu-id="622a9-140">Sign-on URL</span></span> | <span data-ttu-id="622a9-141">Required</span><span class="sxs-lookup"><span data-stu-id="622a9-141">Required</span></span> | <span data-ttu-id="622a9-142">Do not specify</span><span class="sxs-lookup"><span data-stu-id="622a9-142">Do not specify</span></span> | <span data-ttu-id="622a9-143">When a user opens this URL, the service provider redirects to Azure AD to authenticate and sign on the user.</span><span class="sxs-lookup"><span data-stu-id="622a9-143">When a user opens this URL, the service provider redirects to Azure AD to authenticate and sign on the user.</span></span> <span data-ttu-id="622a9-144">Azure AD uses the URL to start the application from Office 365 and the Azure AD Access Panel.</span><span class="sxs-lookup"><span data-stu-id="622a9-144">Azure AD uses the URL to start the application from Office 365 and the Azure AD Access Panel.</span></span> <span data-ttu-id="622a9-145">When blank, Azure AD performs idP-initiated single sign-on when a user launches the application from Office 365, the Azure AD Access Panel, or from the Azure AD single sign-on URL.</span><span class="sxs-lookup"><span data-stu-id="622a9-145">When blank, Azure AD performs idP-initiated single sign-on when a user launches the application from Office 365, the Azure AD Access Panel, or from the Azure AD single sign-on URL.</span></span>|
    | <span data-ttu-id="622a9-146">Identifier (Entity ID)</span><span class="sxs-lookup"><span data-stu-id="622a9-146">Identifier (Entity ID)</span></span> | <span data-ttu-id="622a9-147">Required for some apps</span><span class="sxs-lookup"><span data-stu-id="622a9-147">Required for some apps</span></span> | <span data-ttu-id="622a9-148">Required for some apps</span><span class="sxs-lookup"><span data-stu-id="622a9-148">Required for some apps</span></span> | <span data-ttu-id="622a9-149">Uniquely identifies the application for which single sign-on is being configured.</span><span class="sxs-lookup"><span data-stu-id="622a9-149">Uniquely identifies the application for which single sign-on is being configured.</span></span> <span data-ttu-id="622a9-150">Azure AD sends the identifier back to the application as the Audience parameter of the SAML token, and the application is expected to validate it.</span><span class="sxs-lookup"><span data-stu-id="622a9-150">Azure AD sends the identifier back to the application as the Audience parameter of the SAML token, and the application is expected to validate it.</span></span> <span data-ttu-id="622a9-151">This value also appears as the Entity ID in any SAML metadata provided by the application.</span><span class="sxs-lookup"><span data-stu-id="622a9-151">This value also appears as the Entity ID in any SAML metadata provided by the application.</span></span>|
    | <span data-ttu-id="622a9-152">Reply URL</span><span class="sxs-lookup"><span data-stu-id="622a9-152">Reply URL</span></span> | <span data-ttu-id="622a9-153">Optional</span><span class="sxs-lookup"><span data-stu-id="622a9-153">Optional</span></span> | <span data-ttu-id="622a9-154">Required</span><span class="sxs-lookup"><span data-stu-id="622a9-154">Required</span></span> | <span data-ttu-id="622a9-155">Specifies where the application expects to receive the SAML token.</span><span class="sxs-lookup"><span data-stu-id="622a9-155">Specifies where the application expects to receive the SAML token.</span></span> <span data-ttu-id="622a9-156">The reply URL is also referred to as the Assertion Consumer Service (ACS) URL.</span><span class="sxs-lookup"><span data-stu-id="622a9-156">The reply URL is also referred to as the Assertion Consumer Service (ACS) URL.</span></span> |
    | <span data-ttu-id="622a9-157">Relay State</span><span class="sxs-lookup"><span data-stu-id="622a9-157">Relay State</span></span> | <span data-ttu-id="622a9-158">Optional</span><span class="sxs-lookup"><span data-stu-id="622a9-158">Optional</span></span> | <span data-ttu-id="622a9-159">Optional</span><span class="sxs-lookup"><span data-stu-id="622a9-159">Optional</span></span> | <span data-ttu-id="622a9-160">Specifies to the application where to redirect the user after authentication is completed.</span><span class="sxs-lookup"><span data-stu-id="622a9-160">Specifies to the application where to redirect the user after authentication is completed.</span></span> <span data-ttu-id="622a9-161">Typically the value is a valid URL for the application, however some applications use this field differently.</span><span class="sxs-lookup"><span data-stu-id="622a9-161">Typically the value is a valid URL for the application, however some applications use this field differently.</span></span> <span data-ttu-id="622a9-162">For more information, ask the application vendor.</span><span class="sxs-lookup"><span data-stu-id="622a9-162">For more information, ask the application vendor.</span></span>

2. <span data-ttu-id="622a9-163">Enter the information.</span><span class="sxs-lookup"><span data-stu-id="622a9-163">Enter the information.</span></span> <span data-ttu-id="622a9-164">To see all the settings, click **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="622a9-164">To see all the settings, click **Show advanced URL settings**.</span></span>

    ![Configuration options](media/configure-single-sign-on-portal/config-urls.png)

3. <span data-ttu-id="622a9-166">At the top of the blade, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="622a9-166">At the top of the blade, click **Save**.</span></span>

4. <span data-ttu-id="622a9-167">There is a **Test SAML Settings** button in this section.</span><span class="sxs-lookup"><span data-stu-id="622a9-167">There is a **Test SAML Settings** button in this section.</span></span> <span data-ttu-id="622a9-168">Run this test later in the tutorial in the [Test single sign-on](#test-single-sign-on) section.</span><span class="sxs-lookup"><span data-stu-id="622a9-168">Run this test later in the tutorial in the [Test single sign-on](#test-single-sign-on) section.</span></span>

## <a name="configure-user-attributes"></a><span data-ttu-id="622a9-169">Configure user attributes</span><span class="sxs-lookup"><span data-stu-id="622a9-169">Configure user attributes</span></span>

<span data-ttu-id="622a9-170">User attributes allow you to control what information Azure AD sends to the application.</span><span class="sxs-lookup"><span data-stu-id="622a9-170">User attributes allow you to control what information Azure AD sends to the application.</span></span> <span data-ttu-id="622a9-171">For example, Azure AD could send the name, email, and employee ID of the user to the application.</span><span class="sxs-lookup"><span data-stu-id="622a9-171">For example, Azure AD could send the name, email, and employee ID of the user to the application.</span></span> <span data-ttu-id="622a9-172">Azure AD sends the user attributes to the application in the SAML token each time a user signs-in.</span><span class="sxs-lookup"><span data-stu-id="622a9-172">Azure AD sends the user attributes to the application in the SAML token each time a user signs-in.</span></span> 

<span data-ttu-id="622a9-173">These attributes may be required or optional to make single sign-on work properly.</span><span class="sxs-lookup"><span data-stu-id="622a9-173">These attributes may be required or optional to make single sign-on work properly.</span></span> <span data-ttu-id="622a9-174">For more information, see the [application-specific tutorial](../saas-apps/tutorial-list.md), or ask the application vendor.</span><span class="sxs-lookup"><span data-stu-id="622a9-174">For more information, see the [application-specific tutorial](../saas-apps/tutorial-list.md), or ask the application vendor.</span></span>

1. <span data-ttu-id="622a9-175">To view all the options, click **View and edit all other user attributes**.</span><span class="sxs-lookup"><span data-stu-id="622a9-175">To view all the options, click **View and edit all other user attributes**.</span></span>

    ![Configure user attributes](media/configure-single-sign-on-portal/config-user-attributes.png)

2. <span data-ttu-id="622a9-177">Enter **User Identifier**.</span><span class="sxs-lookup"><span data-stu-id="622a9-177">Enter **User Identifier**.</span></span>

    <span data-ttu-id="622a9-178">The user identifier uniquely identifies each user within the application.</span><span class="sxs-lookup"><span data-stu-id="622a9-178">The user identifier uniquely identifies each user within the application.</span></span> <span data-ttu-id="622a9-179">For example, if the email address is both the username and the unique identifier, set the value to *user.mail*.</span><span class="sxs-lookup"><span data-stu-id="622a9-179">For example, if the email address is both the username and the unique identifier, set the value to *user.mail*.</span></span>

3. <span data-ttu-id="622a9-180">For more SAML token attributes, click **View and edit all other user attributes**.</span><span class="sxs-lookup"><span data-stu-id="622a9-180">For more SAML token attributes, click **View and edit all other user attributes**.</span></span>

4. <span data-ttu-id="622a9-181">To add an attribute to the **SAML Token Attributes**, click **Add attribute**.</span><span class="sxs-lookup"><span data-stu-id="622a9-181">To add an attribute to the **SAML Token Attributes**, click **Add attribute**.</span></span> <span data-ttu-id="622a9-182">Enter the **Name** and select the **Value** from the menu.</span><span class="sxs-lookup"><span data-stu-id="622a9-182">Enter the **Name** and select the **Value** from the menu.</span></span>

5. <span data-ttu-id="622a9-183">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="622a9-183">Click **Save**.</span></span> <span data-ttu-id="622a9-184">You see the new attribute in the table.</span><span class="sxs-lookup"><span data-stu-id="622a9-184">You see the new attribute in the table.</span></span>
 
## <a name="create-a-saml-signing-certificate"></a><span data-ttu-id="622a9-185">Create a SAML signing certificate</span><span class="sxs-lookup"><span data-stu-id="622a9-185">Create a SAML signing certificate</span></span>

<span data-ttu-id="622a9-186">Azure AD uses a certificate to sign the SAML tokens that it sends to the application.</span><span class="sxs-lookup"><span data-stu-id="622a9-186">Azure AD uses a certificate to sign the SAML tokens that it sends to the application.</span></span> 

1. <span data-ttu-id="622a9-187">To see all the options, click **Show advanced certificate signing options**.</span><span class="sxs-lookup"><span data-stu-id="622a9-187">To see all the options, click **Show advanced certificate signing options**.</span></span>

    ![Configure certificates](media/configure-single-sign-on-portal/config-certificate.png)

2. <span data-ttu-id="622a9-189">To configure a certificate, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="622a9-189">To configure a certificate, click **Create new certificate**.</span></span>

3. <span data-ttu-id="622a9-190">In the **Create New Certificate** blade, set the expiration date, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="622a9-190">In the **Create New Certificate** blade, set the expiration date, and click **Save**.</span></span>

4. <span data-ttu-id="622a9-191">Click **Make new certificate active**.</span><span class="sxs-lookup"><span data-stu-id="622a9-191">Click **Make new certificate active**.</span></span>

5. <span data-ttu-id="622a9-192">To learn more, see [Advanced certificate signing options](certificate-signing-options.md).</span><span class="sxs-lookup"><span data-stu-id="622a9-192">To learn more, see [Advanced certificate signing options](certificate-signing-options.md).</span></span>

6. <span data-ttu-id="622a9-193">To keep the changes you have made so far, be sure to click **Save** at the top of the **Single sign-on** blade.</span><span class="sxs-lookup"><span data-stu-id="622a9-193">To keep the changes you have made so far, be sure to click **Save** at the top of the **Single sign-on** blade.</span></span> 

## <a name="assign-users-to-the-application"></a><span data-ttu-id="622a9-194">Assign users to the application</span><span class="sxs-lookup"><span data-stu-id="622a9-194">Assign users to the application</span></span>

<span data-ttu-id="622a9-195">Microsoft recommends testing the single sign-on with several users or groups before rolling out the application to your organization.</span><span class="sxs-lookup"><span data-stu-id="622a9-195">Microsoft recommends testing the single sign-on with several users or groups before rolling out the application to your organization.</span></span>

<span data-ttu-id="622a9-196">To assign a user or group to the application:</span><span class="sxs-lookup"><span data-stu-id="622a9-196">To assign a user or group to the application:</span></span>

1. <span data-ttu-id="622a9-197">Open the application in the portal, if it is not already open.</span><span class="sxs-lookup"><span data-stu-id="622a9-197">Open the application in the portal, if it is not already open.</span></span>
2. <span data-ttu-id="622a9-198">In the left application blade, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="622a9-198">In the left application blade, click **Users and groups**.</span></span>
3. <span data-ttu-id="622a9-199">Click **Add user**.</span><span class="sxs-lookup"><span data-stu-id="622a9-199">Click **Add user**.</span></span>
4. <span data-ttu-id="622a9-200">In the **Add Assignment** blade, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="622a9-200">In the **Add Assignment** blade, click **Users and groups**.</span></span>
5. <span data-ttu-id="622a9-201">To find a specific user, type the user name into the **Select** box, click the checkbox next to the user’s profile photo or logo, and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="622a9-201">To find a specific user, type the user name into the **Select** box, click the checkbox next to the user’s profile photo or logo, and click **Select**.</span></span> 
6. <span data-ttu-id="622a9-202">Find your current username and select it.</span><span class="sxs-lookup"><span data-stu-id="622a9-202">Find your current username and select it.</span></span> <span data-ttu-id="622a9-203">You can optionally select more users.</span><span class="sxs-lookup"><span data-stu-id="622a9-203">You can optionally select more users.</span></span>
7. <span data-ttu-id="622a9-204">In the **Add Assignment** blade, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="622a9-204">In the **Add Assignment** blade, click **Assign**.</span></span> <span data-ttu-id="622a9-205">When completed, the selected users appear in the **Users and groups** list.</span><span class="sxs-lookup"><span data-stu-id="622a9-205">When completed, the selected users appear in the **Users and groups** list.</span></span>

## <a name="configure-the-application-to-use-azure-ad"></a><span data-ttu-id="622a9-206">Configure the application to use Azure AD</span><span class="sxs-lookup"><span data-stu-id="622a9-206">Configure the application to use Azure AD</span></span>

<span data-ttu-id="622a9-207">You're almost done.</span><span class="sxs-lookup"><span data-stu-id="622a9-207">You're almost done.</span></span>  <span data-ttu-id="622a9-208">As a final step, you need to configure the application to use Azure AD as a SAML identity provider.</span><span class="sxs-lookup"><span data-stu-id="622a9-208">As a final step, you need to configure the application to use Azure AD as a SAML identity provider.</span></span> 

1. <span data-ttu-id="622a9-209">Scroll down to the end of the **Single sign-on** blade for your application.</span><span class="sxs-lookup"><span data-stu-id="622a9-209">Scroll down to the end of the **Single sign-on** blade for your application.</span></span> 

    ![Configure application](media/configure-single-sign-on-portal/configure-app.png)

2. <span data-ttu-id="622a9-211">Click **Configure application** in the portal, and follow the instructions.</span><span class="sxs-lookup"><span data-stu-id="622a9-211">Click **Configure application** in the portal, and follow the instructions.</span></span>
3. <span data-ttu-id="622a9-212">Manually create user accounts in the application for the purpose of testing single sign-on.</span><span class="sxs-lookup"><span data-stu-id="622a9-212">Manually create user accounts in the application for the purpose of testing single sign-on.</span></span> <span data-ttu-id="622a9-213">Create the user accounts you assigned to the application in the [previous section](#assign-users-to-the-application).</span><span class="sxs-lookup"><span data-stu-id="622a9-213">Create the user accounts you assigned to the application in the [previous section](#assign-users-to-the-application).</span></span>   <span data-ttu-id="622a9-214">When you are ready to roll out the application to the organization, we recommend using automatic user provisioning to automatically create user accounts in the application.</span><span class="sxs-lookup"><span data-stu-id="622a9-214">When you are ready to roll out the application to the organization, we recommend using automatic user provisioning to automatically create user accounts in the application.</span></span>

## <a name="test-single-sign-on"></a><span data-ttu-id="622a9-215">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="622a9-215">Test single sign-on</span></span>

<span data-ttu-id="622a9-216">You are ready to test your settings.</span><span class="sxs-lookup"><span data-stu-id="622a9-216">You are ready to test your settings.</span></span>  

1. <span data-ttu-id="622a9-217">Open the single sign-on settings for your application.</span><span class="sxs-lookup"><span data-stu-id="622a9-217">Open the single sign-on settings for your application.</span></span> 
2. <span data-ttu-id="622a9-218">Scroll to the **Configure domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="622a9-218">Scroll to the **Configure domain and URLs** section.</span></span>
2. <span data-ttu-id="622a9-219">Click **Test SAML Settings**.</span><span class="sxs-lookup"><span data-stu-id="622a9-219">Click **Test SAML Settings**.</span></span> <span data-ttu-id="622a9-220">The testing options appear.</span><span class="sxs-lookup"><span data-stu-id="622a9-220">The testing options appear.</span></span>

    ![Test single sign-on options](media/configure-single-sign-on-portal/test-single-sign-on.png) 

3. <span data-ttu-id="622a9-222">Click **Sign in as current user**.</span><span class="sxs-lookup"><span data-stu-id="622a9-222">Click **Sign in as current user**.</span></span> <span data-ttu-id="622a9-223">This lets you first see if single sign-on works for you, the admin.</span><span class="sxs-lookup"><span data-stu-id="622a9-223">This lets you first see if single sign-on works for you, the admin.</span></span>
4. <span data-ttu-id="622a9-224">If there is an error, an error message appears.</span><span class="sxs-lookup"><span data-stu-id="622a9-224">If there is an error, an error message appears.</span></span> <span data-ttu-id="622a9-225">Copy and paste the specifics into the **What does the error look like?** box.</span><span class="sxs-lookup"><span data-stu-id="622a9-225">Copy and paste the specifics into the **What does the error look like?** box.</span></span>

    ![Get resolution guidance](media/configure-single-sign-on-portal/error-guidance.png)

5. <span data-ttu-id="622a9-227">Click **Get resolution guidance**.</span><span class="sxs-lookup"><span data-stu-id="622a9-227">Click **Get resolution guidance**.</span></span> <span data-ttu-id="622a9-228">Root cause and resolution guidance appears.</span><span class="sxs-lookup"><span data-stu-id="622a9-228">Root cause and resolution guidance appears.</span></span>  <span data-ttu-id="622a9-229">In this example, the user was not assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="622a9-229">In this example, the user was not assigned to the application.</span></span>

    ![Fix error](media/configure-single-sign-on-portal/fix-error.png)

6. <span data-ttu-id="622a9-231">Read the resolution guidance and then, if appropriate, click **Fix it**.</span><span class="sxs-lookup"><span data-stu-id="622a9-231">Read the resolution guidance and then, if appropriate, click **Fix it**.</span></span>

7. <span data-ttu-id="622a9-232">Run the test again until it completes successfully.</span><span class="sxs-lookup"><span data-stu-id="622a9-232">Run the test again until it completes successfully.</span></span>



## <a name="next-steps"></a><span data-ttu-id="622a9-233">Next steps</span><span class="sxs-lookup"><span data-stu-id="622a9-233">Next steps</span></span>
<span data-ttu-id="622a9-234">In this tutorial, you used the Azure portal to configure an application for single sign-on with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="622a9-234">In this tutorial, you used the Azure portal to configure an application for single sign-on with Azure AD.</span></span> <span data-ttu-id="622a9-235">You found the single sign-on configuration page, and configured the single sign-on settings.</span><span class="sxs-lookup"><span data-stu-id="622a9-235">You found the single sign-on configuration page, and configured the single sign-on settings.</span></span> <span data-ttu-id="622a9-236">After finishing the configuration, you assigned a user to the application, and configured the application to use SAML-based single sign-on.</span><span class="sxs-lookup"><span data-stu-id="622a9-236">After finishing the configuration, you assigned a user to the application, and configured the application to use SAML-based single sign-on.</span></span> <span data-ttu-id="622a9-237">When all of this work was finished, you verified the SAML sign-on is working properly.</span><span class="sxs-lookup"><span data-stu-id="622a9-237">When all of this work was finished, you verified the SAML sign-on is working properly.</span></span>

<span data-ttu-id="622a9-238">You did these things:</span><span class="sxs-lookup"><span data-stu-id="622a9-238">You did these things:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="622a9-239">Selected SAML for the single sign-on mode</span><span class="sxs-lookup"><span data-stu-id="622a9-239">Selected SAML for the single sign-on mode</span></span>
> * <span data-ttu-id="622a9-240">Contacted the application vendor to configure domain and URLs</span><span class="sxs-lookup"><span data-stu-id="622a9-240">Contacted the application vendor to configure domain and URLs</span></span>
> * <span data-ttu-id="622a9-241">Configured user attributes</span><span class="sxs-lookup"><span data-stu-id="622a9-241">Configured user attributes</span></span>
> * <span data-ttu-id="622a9-242">Created a SAML signing certificate</span><span class="sxs-lookup"><span data-stu-id="622a9-242">Created a SAML signing certificate</span></span>
> * <span data-ttu-id="622a9-243">Manually assigned users or groups to the application</span><span class="sxs-lookup"><span data-stu-id="622a9-243">Manually assigned users or groups to the application</span></span>
> * <span data-ttu-id="622a9-244">Configured the application for single sign-on</span><span class="sxs-lookup"><span data-stu-id="622a9-244">Configured the application for single sign-on</span></span>
> * <span data-ttu-id="622a9-245">Tested the SAML-based single sign-on</span><span class="sxs-lookup"><span data-stu-id="622a9-245">Tested the SAML-based single sign-on</span></span>

<span data-ttu-id="622a9-246">To roll out the application to more users in your organization, we recommend using automatic provisioning.</span><span class="sxs-lookup"><span data-stu-id="622a9-246">To roll out the application to more users in your organization, we recommend using automatic provisioning.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="622a9-247">Learn how to assign users with automatic provisioning</span><span class="sxs-lookup"><span data-stu-id="622a9-247">Learn how to assign users with automatic provisioning</span></span>](configure-automatic-user-provisioning-portal.md)


