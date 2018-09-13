---
title: 'Tutorial: Azure Active Directory integration with Help Scout | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Help Scout.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/14/2017
ms.author: jeedes
ms.openlocfilehash: 0bbdf576c38207349bb45e7b54f3ffc85ecf3d36
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856594"
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a><span data-ttu-id="319ac-103">Tutorial: Azure Active Directory integration with Help Scout</span><span class="sxs-lookup"><span data-stu-id="319ac-103">Tutorial: Azure Active Directory integration with Help Scout</span></span>

<span data-ttu-id="319ac-104">In this tutorial, you learn how to integrate Help Scout with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="319ac-104">In this tutorial, you learn how to integrate Help Scout with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="319ac-105">Integrating Help Scout with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="319ac-105">Integrating Help Scout with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="319ac-106">You can control in Azure AD who has access to Help Scout.</span><span class="sxs-lookup"><span data-stu-id="319ac-106">You can control in Azure AD who has access to Help Scout.</span></span>
- <span data-ttu-id="319ac-107">You can enable your users to automatically get signed-on to Help Scout (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="319ac-107">You can enable your users to automatically get signed-on to Help Scout (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="319ac-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="319ac-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="319ac-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="319ac-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="319ac-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="319ac-110">Prerequisites</span></span>

<span data-ttu-id="319ac-111">To configure Azure AD integration with Help Scout, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="319ac-111">To configure Azure AD integration with Help Scout, you need the following items:</span></span>

- <span data-ttu-id="319ac-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="319ac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="319ac-113">A Help Scout single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="319ac-113">A Help Scout single-sign on enabled subscription</span></span>

<span data-ttu-id="319ac-114">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="319ac-114">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="319ac-115">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="319ac-115">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="319ac-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="319ac-116">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="319ac-117">Scenario description</span><span class="sxs-lookup"><span data-stu-id="319ac-117">Scenario description</span></span>
<span data-ttu-id="319ac-118">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="319ac-118">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="319ac-119">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="319ac-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="319ac-120">Adding Help Scout from the gallery</span><span class="sxs-lookup"><span data-stu-id="319ac-120">Adding Help Scout from the gallery</span></span>
1. <span data-ttu-id="319ac-121">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="319ac-121">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-help-scout-from-the-gallery"></a><span data-ttu-id="319ac-122">Adding Help Scout from the gallery</span><span class="sxs-lookup"><span data-stu-id="319ac-122">Adding Help Scout from the gallery</span></span>
<span data-ttu-id="319ac-123">To configure the integration of Help Scout into Azure AD, you need to add Help Scout from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="319ac-123">To configure the integration of Help Scout into Azure AD, you need to add Help Scout from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="319ac-124">**To add Help Scout from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="319ac-124">**To add Help Scout from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="319ac-125">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="319ac-125">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="319ac-127">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="319ac-127">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="319ac-128">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="319ac-128">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="319ac-130">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="319ac-130">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="319ac-132">In the search box, type **Help Scout**, select **Help Scout** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="319ac-132">In the search box, type **Help Scout**, select **Help Scout** from result panel then click **Add** button to add the application.</span></span>

    ![Help Scout in the results list](./media/helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="319ac-134">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="319ac-134">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="319ac-135">In this section, you configure and test Azure AD single sign-on with Help Scout based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="319ac-135">In this section, you configure and test Azure AD single sign-on with Help Scout based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="319ac-136">For single sign-on to work, Azure AD needs to know what the counterpart user in Help Scout is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="319ac-136">For single sign-on to work, Azure AD needs to know what the counterpart user in Help Scout is to a user in Azure AD.</span></span> <span data-ttu-id="319ac-137">In other words, a link relationship between an Azure AD user and the related user in Help Scout needs to be established.</span><span class="sxs-lookup"><span data-stu-id="319ac-137">In other words, a link relationship between an Azure AD user and the related user in Help Scout needs to be established.</span></span>

<span data-ttu-id="319ac-138">Help Scout uses email addresses for logins, so to establish the link relationship, use the same **email address** as **user name** in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="319ac-138">Help Scout uses email addresses for logins, so to establish the link relationship, use the same **email address** as **user name** in Azure AD.</span></span>

<span data-ttu-id="319ac-139">To configure and test Azure AD single sign-on with Help Scout, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="319ac-139">To configure and test Azure AD single sign-on with Help Scout, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="319ac-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="319ac-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="319ac-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="319ac-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="319ac-142">**[Create a Help Scout test user](#create-a-help-scout-test-user)** - to have a counterpart of Britta Simon in Help Scout that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="319ac-142">**[Create a Help Scout test user](#create-a-help-scout-test-user)** - to have a counterpart of Britta Simon in Help Scout that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="319ac-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="319ac-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="319ac-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="319ac-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="319ac-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="319ac-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="319ac-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Help Scout application.</span><span class="sxs-lookup"><span data-stu-id="319ac-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Help Scout application.</span></span>

<span data-ttu-id="319ac-147">**To configure Azure AD single sign-on with Help Scout, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="319ac-147">**To configure Azure AD single sign-on with Help Scout, perform the following steps:**</span></span>

1. <span data-ttu-id="319ac-148">In the Azure portal, on the **Help Scout** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="319ac-148">In the Azure portal, on the **Help Scout** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="319ac-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="319ac-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/helpscout-tutorial/tutorial_helpscout_samlbase.png)

1. <span data-ttu-id="319ac-152">On the **Help Scout Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="319ac-152">On the **Help Scout Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Help Scout Domain and URLs single sign-on information](./media/helpscout-tutorial/tutorial_helpscout_url.png)

    <span data-ttu-id="319ac-154">a.</span><span class="sxs-lookup"><span data-stu-id="319ac-154">a.</span></span> <span data-ttu-id="319ac-155">**Identifier** is the **"Audience URI (Service Provider Entity ID)"** from Help Scout, starts with `urn:`</span><span class="sxs-lookup"><span data-stu-id="319ac-155">**Identifier** is the **"Audience URI (Service Provider Entity ID)"** from Help Scout, starts with `urn:`</span></span>

    <span data-ttu-id="319ac-156">b.</span><span class="sxs-lookup"><span data-stu-id="319ac-156">b.</span></span> <span data-ttu-id="319ac-157">**Reply URL** is the **"Post-back URL (Assertion Consumer Service URL)"** from Help Scout, starts with `https://`</span><span class="sxs-lookup"><span data-stu-id="319ac-157">**Reply URL** is the **"Post-back URL (Assertion Consumer Service URL)"** from Help Scout, starts with `https://`</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="319ac-158">The values in these URLs are for demonstration only.</span><span class="sxs-lookup"><span data-stu-id="319ac-158">The values in these URLs are for demonstration only.</span></span> <span data-ttu-id="319ac-159">You need to update these values from actual Reply URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="319ac-159">You need to update these values from actual Reply URL and Identifier.</span></span> <span data-ttu-id="319ac-160">You get these values from the **Single Sign-On** tab under Authentication section, which is explained later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="319ac-160">You get these values from the **Single Sign-On** tab under Authentication section, which is explained later in the tutorial.</span></span>

1. <span data-ttu-id="319ac-161">If you wish to configure the application in **SP** initiated mode, check **Show advanced URL settings** and perform the following step:</span><span class="sxs-lookup"><span data-stu-id="319ac-161">If you wish to configure the application in **SP** initiated mode, check **Show advanced URL settings** and perform the following step:</span></span>

    ![Help Scout Domain and URLs single sign-on information](./media/helpscout-tutorial/tutorial_helpscout_url1.png)

    <span data-ttu-id="319ac-163">In the **Sign-on URL** textbox, type a URL as: `https://secure.helpscout.net/members/login/`</span><span class="sxs-lookup"><span data-stu-id="319ac-163">In the **Sign-on URL** textbox, type a URL as: `https://secure.helpscout.net/members/login/`</span></span>
     
1. <span data-ttu-id="319ac-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="319ac-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/helpscout-tutorial/tutorial_helpscout_certificate.png) 

1. <span data-ttu-id="319ac-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="319ac-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/helpscout-tutorial/tutorial_general_400.png)


1. <span data-ttu-id="319ac-168">On the **Help Scout Configuration** section, click **Configure Help Scout** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="319ac-168">On the **Help Scout Configuration** section, click **Configure Help Scout** to open **Configure sign-on** window.</span></span> <span data-ttu-id="319ac-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section**.</span><span class="sxs-lookup"><span data-stu-id="319ac-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section**.</span></span>

    ![Configure Single Sign-On](./media/helpscout-tutorial/config.png) 

1. <span data-ttu-id="319ac-171">In a different web browser window, log in to your Help Scout company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="319ac-171">In a different web browser window, log in to your Help Scout company site as an administrator.</span></span>

1. <span data-ttu-id="319ac-172">Once you are logged in click on **"Manage"** from the top menu and then select **"Company"** from the dropdown menu.</span><span class="sxs-lookup"><span data-stu-id="319ac-172">Once you are logged in click on **"Manage"** from the top menu and then select **"Company"** from the dropdown menu.</span></span>

    ![Configure Single Sign-On](./media/helpscout-tutorial/settings1.png) 
 
1. <span data-ttu-id="319ac-174">Select **"Authentication"** from the left-hand menu.</span><span class="sxs-lookup"><span data-stu-id="319ac-174">Select **"Authentication"** from the left-hand menu.</span></span> 

    ![Configure Single Sign-On](./media/helpscout-tutorial/settings2.png) 

1. <span data-ttu-id="319ac-176">This takes you to the SAML settings section and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="319ac-176">This takes you to the SAML settings section and perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/helpscout-tutorial/settings3.png) 
 
    <span data-ttu-id="319ac-178">a.</span><span class="sxs-lookup"><span data-stu-id="319ac-178">a.</span></span> <span data-ttu-id="319ac-179">Copy the **Post-back URL (Assertion Consumer Service URL)** value and paste the value in the **Reply URL** box in the Azure portal, under Help Scout **Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="319ac-179">Copy the **Post-back URL (Assertion Consumer Service URL)** value and paste the value in the **Reply URL** box in the Azure portal, under Help Scout **Domain and URLs** section.</span></span>
    
    <span data-ttu-id="319ac-180">b.</span><span class="sxs-lookup"><span data-stu-id="319ac-180">b.</span></span> <span data-ttu-id="319ac-181">Copy the **Audience URI (Service Provider Entity ID)** value and paste the value in the **Identifier** box in the Azure portal, under Help Scout **Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="319ac-181">Copy the **Audience URI (Service Provider Entity ID)** value and paste the value in the **Identifier** box in the Azure portal, under Help Scout **Domain and URLs** section.</span></span>

1. <span data-ttu-id="319ac-182">Toggle **Enable SAML** on and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="319ac-182">Toggle **Enable SAML** on and perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/helpscout-tutorial/settings4.png) 
 
    <span data-ttu-id="319ac-184">a.</span><span class="sxs-lookup"><span data-stu-id="319ac-184">a.</span></span> <span data-ttu-id="319ac-185">In **Single Sign-On URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="319ac-185">In **Single Sign-On URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="319ac-186">b.</span><span class="sxs-lookup"><span data-stu-id="319ac-186">b.</span></span> <span data-ttu-id="319ac-187">Click **Upload Certificate** to upload the **Certificate(Base64)** downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="319ac-187">Click **Upload Certificate** to upload the **Certificate(Base64)** downloaded from Azure portal.</span></span>

    <span data-ttu-id="319ac-188">c.</span><span class="sxs-lookup"><span data-stu-id="319ac-188">c.</span></span> <span data-ttu-id="319ac-189">Enter your organization's email domain(s) e.x.- `contoso.com` in the **Email Domains** textbox.</span><span class="sxs-lookup"><span data-stu-id="319ac-189">Enter your organization's email domain(s) e.x.- `contoso.com` in the **Email Domains** textbox.</span></span> <span data-ttu-id="319ac-190">You can separate multiple domains with a comma.</span><span class="sxs-lookup"><span data-stu-id="319ac-190">You can separate multiple domains with a comma.</span></span> <span data-ttu-id="319ac-191">Anytime a Help Scout User or Administrator who enters that specific domain on the [Help Scout log-in page](https://secure.helpscout.net/members/login/) will be routed to Identity Provider to authenticate with their credentials.</span><span class="sxs-lookup"><span data-stu-id="319ac-191">Anytime a Help Scout User or Administrator who enters that specific domain on the [Help Scout log-in page](https://secure.helpscout.net/members/login/) will be routed to Identity Provider to authenticate with their credentials.</span></span>

    <span data-ttu-id="319ac-192">d.</span><span class="sxs-lookup"><span data-stu-id="319ac-192">d.</span></span> <span data-ttu-id="319ac-193">Lastly, you can toggle **Force SAML Sign-on** if you want Users to only log in to Help Scout via through this method.</span><span class="sxs-lookup"><span data-stu-id="319ac-193">Lastly, you can toggle **Force SAML Sign-on** if you want Users to only log in to Help Scout via through this method.</span></span> <span data-ttu-id="319ac-194">If you'd still like to leave the option for them to sign in with their Help Scout credentials, you can leave it toggled off.</span><span class="sxs-lookup"><span data-stu-id="319ac-194">If you'd still like to leave the option for them to sign in with their Help Scout credentials, you can leave it toggled off.</span></span> <span data-ttu-id="319ac-195">Even if this is enabled, an Account Owner will always be able to log in to Help Scout with their account password.</span><span class="sxs-lookup"><span data-stu-id="319ac-195">Even if this is enabled, an Account Owner will always be able to log in to Help Scout with their account password.</span></span>

    <span data-ttu-id="319ac-196">e.</span><span class="sxs-lookup"><span data-stu-id="319ac-196">e.</span></span> <span data-ttu-id="319ac-197">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="319ac-197">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="319ac-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="319ac-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="319ac-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="319ac-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="319ac-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="319ac-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="319ac-201">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="319ac-201">Create an Azure AD test user</span></span>

<span data-ttu-id="319ac-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="319ac-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="319ac-204">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="319ac-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="319ac-205">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="319ac-205">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/helpscout-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="319ac-207">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="319ac-207">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/helpscout-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="319ac-209">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="319ac-209">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/helpscout-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="319ac-211">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="319ac-211">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/helpscout-tutorial/create_aaduser_04.png)

    <span data-ttu-id="319ac-213">a.</span><span class="sxs-lookup"><span data-stu-id="319ac-213">a.</span></span> <span data-ttu-id="319ac-214">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="319ac-214">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="319ac-215">b.</span><span class="sxs-lookup"><span data-stu-id="319ac-215">b.</span></span> <span data-ttu-id="319ac-216">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="319ac-216">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="319ac-217">c.</span><span class="sxs-lookup"><span data-stu-id="319ac-217">c.</span></span> <span data-ttu-id="319ac-218">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="319ac-218">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="319ac-219">d.</span><span class="sxs-lookup"><span data-stu-id="319ac-219">d.</span></span> <span data-ttu-id="319ac-220">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="319ac-220">Click **Create**.</span></span>
 
### <a name="create-a-help-scout-test-user"></a><span data-ttu-id="319ac-221">Create a Help Scout test user</span><span class="sxs-lookup"><span data-stu-id="319ac-221">Create a Help Scout test user</span></span>

<span data-ttu-id="319ac-222">The objective of this section is to create a user called Britta Simon in Help Scout.</span><span class="sxs-lookup"><span data-stu-id="319ac-222">The objective of this section is to create a user called Britta Simon in Help Scout.</span></span> <span data-ttu-id="319ac-223">Help Scout supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="319ac-223">Help Scout supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="319ac-224">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="319ac-224">There is no action item for you in this section.</span></span> <span data-ttu-id="319ac-225">If a user doesn't already exist in Help Scout, a new one is created when you attempt to access Help Scout.</span><span class="sxs-lookup"><span data-stu-id="319ac-225">If a user doesn't already exist in Help Scout, a new one is created when you attempt to access Help Scout.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="319ac-226">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="319ac-226">Assign the Azure AD test user</span></span>

<span data-ttu-id="319ac-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Help Scout.</span><span class="sxs-lookup"><span data-stu-id="319ac-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Help Scout.</span></span>

![Assign the user role][200] 

<span data-ttu-id="319ac-229">**To assign Britta Simon to Help Scout, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="319ac-229">**To assign Britta Simon to Help Scout, perform the following steps:**</span></span>

1. <span data-ttu-id="319ac-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="319ac-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="319ac-232">In the applications list, select **Help Scout**.</span><span class="sxs-lookup"><span data-stu-id="319ac-232">In the applications list, select **Help Scout**.</span></span>

    ![The Help Scout link in the Applications list](./media/helpscout-tutorial/tutorial_helpscout_app.png)  

1. <span data-ttu-id="319ac-234">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="319ac-234">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="319ac-236">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="319ac-236">Click **Add** button.</span></span> <span data-ttu-id="319ac-237">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="319ac-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="319ac-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="319ac-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="319ac-240">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="319ac-240">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="319ac-241">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="319ac-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="319ac-242">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="319ac-242">Test single sign-on</span></span>

<span data-ttu-id="319ac-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="319ac-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="319ac-244">When you click the Help Scout tile in the Access Panel, you should get automatically signed-on to your Help Scout application.</span><span class="sxs-lookup"><span data-stu-id="319ac-244">When you click the Help Scout tile in the Access Panel, you should get automatically signed-on to your Help Scout application.</span></span>
<span data-ttu-id="319ac-245">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="319ac-245">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="319ac-246">Additional resources</span><span class="sxs-lookup"><span data-stu-id="319ac-246">Additional resources</span></span>

* [<span data-ttu-id="319ac-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="319ac-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="319ac-248">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="319ac-248">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/helpscout-tutorial/tutorial_general_01.png
[2]: ./media/helpscout-tutorial/tutorial_general_02.png
[3]: ./media/helpscout-tutorial/tutorial_general_03.png
[4]: ./media/helpscout-tutorial/tutorial_general_04.png

[100]: ./media/helpscout-tutorial/tutorial_general_100.png

[200]: ./media/helpscout-tutorial/tutorial_general_200.png
[201]: ./media/helpscout-tutorial/tutorial_general_201.png
[202]: ./media/helpscout-tutorial/tutorial_general_202.png
[203]: ./media/helpscout-tutorial/tutorial_general_203.png

