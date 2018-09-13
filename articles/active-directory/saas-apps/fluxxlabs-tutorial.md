---
title: 'Tutorial: Azure Active Directory integration with Fluxx Labs | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Fluxx Labs.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d8fac770-bb57-4e1f-b50b-9ffeae239d07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2018
ms.author: jeedes
ms.openlocfilehash: 367310527619d4bdb5f84a80c567a9d83698846e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866571"
---
# <a name="tutorial-azure-active-directory-integration-with-fluxx-labs"></a><span data-ttu-id="fb90b-103">Tutorial: Azure Active Directory integration with Fluxx Labs</span><span class="sxs-lookup"><span data-stu-id="fb90b-103">Tutorial: Azure Active Directory integration with Fluxx Labs</span></span>

<span data-ttu-id="fb90b-104">In this tutorial, you learn how to integrate Fluxx Labs with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fb90b-104">In this tutorial, you learn how to integrate Fluxx Labs with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fb90b-105">Integrating Fluxx Labs with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="fb90b-105">Integrating Fluxx Labs with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fb90b-106">You can control in Azure AD who has access to Fluxx Labs.</span><span class="sxs-lookup"><span data-stu-id="fb90b-106">You can control in Azure AD who has access to Fluxx Labs.</span></span>
- <span data-ttu-id="fb90b-107">You can enable your users to automatically get signed-on to Fluxx Labs (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="fb90b-107">You can enable your users to automatically get signed-on to Fluxx Labs (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fb90b-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fb90b-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="fb90b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="fb90b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb90b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fb90b-110">Prerequisites</span></span>

<span data-ttu-id="fb90b-111">To configure Azure AD integration with Fluxx Labs, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="fb90b-111">To configure Azure AD integration with Fluxx Labs, you need the following items:</span></span>

- <span data-ttu-id="fb90b-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="fb90b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fb90b-113">A Fluxx Labs single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="fb90b-113">A Fluxx Labs single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fb90b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="fb90b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fb90b-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="fb90b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fb90b-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="fb90b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fb90b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fb90b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fb90b-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="fb90b-118">Scenario description</span></span>
<span data-ttu-id="fb90b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="fb90b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fb90b-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="fb90b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fb90b-121">Adding Fluxx Labs from the gallery</span><span class="sxs-lookup"><span data-stu-id="fb90b-121">Adding Fluxx Labs from the gallery</span></span>
1. <span data-ttu-id="fb90b-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fb90b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fluxx-labs-from-the-gallery"></a><span data-ttu-id="fb90b-123">Adding Fluxx Labs from the gallery</span><span class="sxs-lookup"><span data-stu-id="fb90b-123">Adding Fluxx Labs from the gallery</span></span>
<span data-ttu-id="fb90b-124">To configure the integration of Fluxx Labs into Azure AD, you need to add Fluxx Labs from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="fb90b-124">To configure the integration of Fluxx Labs into Azure AD, you need to add Fluxx Labs from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fb90b-125">**To add Fluxx Labs from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fb90b-125">**To add Fluxx Labs from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fb90b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="fb90b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="fb90b-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="fb90b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fb90b-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="fb90b-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

1. <span data-ttu-id="fb90b-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="fb90b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="fb90b-133">In the search box, type **Fluxx Labs**, select **Fluxx Labs** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="fb90b-133">In the search box, type **Fluxx Labs**, select **Fluxx Labs** from result panel then click **Add** button to add the application.</span></span>

    ![Fluxx Labs in the results list](./media/fluxxlabs-tutorial/tutorial_fluxxlabs_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fb90b-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fb90b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="fb90b-136">In this section, you configure and test Azure AD single sign-on with Fluxx Labs based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="fb90b-136">In this section, you configure and test Azure AD single sign-on with Fluxx Labs based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fb90b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Fluxx Labs is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb90b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Fluxx Labs is to a user in Azure AD.</span></span> <span data-ttu-id="fb90b-138">In other words, a link relationship between an Azure AD user and the related user in Fluxx Labs needs to be established.</span><span class="sxs-lookup"><span data-stu-id="fb90b-138">In other words, a link relationship between an Azure AD user and the related user in Fluxx Labs needs to be established.</span></span>

<span data-ttu-id="fb90b-139">In Fluxx Labs, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="fb90b-139">In Fluxx Labs, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fb90b-140">To configure and test Azure AD single sign-on with Fluxx Labs, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="fb90b-140">To configure and test Azure AD single sign-on with Fluxx Labs, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fb90b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="fb90b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="fb90b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fb90b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="fb90b-143">**[Create a Fluxx Labs test user](#create-a-fluxx-labs-test-user)** - to have a counterpart of Britta Simon in Fluxx Labs that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="fb90b-143">**[Create a Fluxx Labs test user](#create-a-fluxx-labs-test-user)** - to have a counterpart of Britta Simon in Fluxx Labs that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="fb90b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fb90b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="fb90b-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="fb90b-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="fb90b-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="fb90b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="fb90b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Fluxx Labs application.</span><span class="sxs-lookup"><span data-stu-id="fb90b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Fluxx Labs application.</span></span>

<span data-ttu-id="fb90b-148">**To configure Azure AD single sign-on with Fluxx Labs, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fb90b-148">**To configure Azure AD single sign-on with Fluxx Labs, perform the following steps:**</span></span>

1. <span data-ttu-id="fb90b-149">In the Azure portal, on the **Fluxx Labs** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="fb90b-149">In the Azure portal, on the **Fluxx Labs** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="fb90b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="fb90b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/fluxxlabs-tutorial/tutorial_fluxxlabs_samlbase.png)

1. <span data-ttu-id="fb90b-153">On the **Fluxx Labs Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fb90b-153">On the **Fluxx Labs Domain and URLs** section, perform the following steps:</span></span>

    ![Fluxx Labs Domain and URLs single sign-on information](./media/fluxxlabs-tutorial/tutorial_fluxxlabs_url.png)

    <span data-ttu-id="fb90b-155">a.</span><span class="sxs-lookup"><span data-stu-id="fb90b-155">a.</span></span> <span data-ttu-id="fb90b-156">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="fb90b-156">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    | <span data-ttu-id="fb90b-157">Environment</span><span class="sxs-lookup"><span data-stu-id="fb90b-157">Environment</span></span> | <span data-ttu-id="fb90b-158">URL Pattern</span><span class="sxs-lookup"><span data-stu-id="fb90b-158">URL Pattern</span></span>|
    |-------------|------------|
    | <span data-ttu-id="fb90b-159">Production</span><span class="sxs-lookup"><span data-stu-id="fb90b-159">Production</span></span> | `https://<subdomain>.fluxx.io` |
    | <span data-ttu-id="fb90b-160">Pre production</span><span class="sxs-lookup"><span data-stu-id="fb90b-160">Pre production</span></span> | `https://<subdomain>.preprod.fluxxlabs.com`|
        
    <span data-ttu-id="fb90b-161">b.</span><span class="sxs-lookup"><span data-stu-id="fb90b-161">b.</span></span> <span data-ttu-id="fb90b-162">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="fb90b-162">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>

    | <span data-ttu-id="fb90b-163">Environment</span><span class="sxs-lookup"><span data-stu-id="fb90b-163">Environment</span></span> | <span data-ttu-id="fb90b-164">URL Pattern</span><span class="sxs-lookup"><span data-stu-id="fb90b-164">URL Pattern</span></span>|
    |-------------|------------|
    | <span data-ttu-id="fb90b-165">Production</span><span class="sxs-lookup"><span data-stu-id="fb90b-165">Production</span></span> | `https://<subdomain>.fluxx.io/auth/saml/callback` |
    | <span data-ttu-id="fb90b-166">Pre production</span><span class="sxs-lookup"><span data-stu-id="fb90b-166">Pre production</span></span> | `https://<subdomain>.preprod.fluxxlabs.com/auth/saml/callback`|

    > [!NOTE]
    > <span data-ttu-id="fb90b-167">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="fb90b-167">These values are not real.</span></span> <span data-ttu-id="fb90b-168">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="fb90b-168">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="fb90b-169">Contact [Fluxx Labs support team](mailto:travis@fluxxlabs.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="fb90b-169">Contact [Fluxx Labs support team](mailto:travis@fluxxlabs.com) to get these values.</span></span>

1. <span data-ttu-id="fb90b-170">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="fb90b-170">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/fluxxlabs-tutorial/tutorial_fluxxlabs_certificate.png) 

1. <span data-ttu-id="fb90b-172">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="fb90b-172">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/fluxxlabs-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="fb90b-174">On the **Fluxx Labs Configuration** section, click **Configure Fluxx Labs** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="fb90b-174">On the **Fluxx Labs Configuration** section, click **Configure Fluxx Labs** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fb90b-175">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="fb90b-175">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Fluxx Labs Configuration](./media/fluxxlabs-tutorial/tutorial_fluxxlabs_configure.png)

1. <span data-ttu-id="fb90b-177">In a different web browser window, sign on to your Fluxx Labs company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="fb90b-177">In a different web browser window, sign on to your Fluxx Labs company site as administrator.</span></span>

1. <span data-ttu-id="fb90b-178">Select **Admin** below the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="fb90b-178">Select **Admin** below the **Settings** section.</span></span>

    ![Fluxx Labs Configuration](./media/fluxxlabs-tutorial/config1.png)

1. <span data-ttu-id="fb90b-180">In the Admin Panel, Select **Plug-ins** > **Integrations** and then select **SAML SSO-(Disabled)**</span><span class="sxs-lookup"><span data-stu-id="fb90b-180">In the Admin Panel, Select **Plug-ins** > **Integrations** and then select **SAML SSO-(Disabled)**</span></span>

    ![Fluxx Labs Configuration](./media/fluxxlabs-tutorial/config2.png)

1. <span data-ttu-id="fb90b-182">In the attribute section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fb90b-182">In the attribute section, perform the following steps:</span></span>

    ![Fluxx Labs Configuration](./media/fluxxlabs-tutorial/config3.png)

    <span data-ttu-id="fb90b-184">a.</span><span class="sxs-lookup"><span data-stu-id="fb90b-184">a.</span></span> <span data-ttu-id="fb90b-185">Select the **SAML SSO** checkbox.</span><span class="sxs-lookup"><span data-stu-id="fb90b-185">Select the **SAML SSO** checkbox.</span></span>

    <span data-ttu-id="fb90b-186">b.</span><span class="sxs-lookup"><span data-stu-id="fb90b-186">b.</span></span> <span data-ttu-id="fb90b-187">In the **Request Path** textbox, type **/auth/saml**.</span><span class="sxs-lookup"><span data-stu-id="fb90b-187">In the **Request Path** textbox, type **/auth/saml**.</span></span>

    <span data-ttu-id="fb90b-188">c.</span><span class="sxs-lookup"><span data-stu-id="fb90b-188">c.</span></span> <span data-ttu-id="fb90b-189">In the **Callback Path** textbox, type **/auth/saml/callback**.</span><span class="sxs-lookup"><span data-stu-id="fb90b-189">In the **Callback Path** textbox, type **/auth/saml/callback**.</span></span>

    <span data-ttu-id="fb90b-190">d.</span><span class="sxs-lookup"><span data-stu-id="fb90b-190">d.</span></span> <span data-ttu-id="fb90b-191">In the **Assertion Consumer Service Url(Single Sign-On URL)** textbox, enter the **Reply URL** value, which you have entered in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fb90b-191">In the **Assertion Consumer Service Url(Single Sign-On URL)** textbox, enter the **Reply URL** value, which you have entered in the Azure portal.</span></span>

    <span data-ttu-id="fb90b-192">e.</span><span class="sxs-lookup"><span data-stu-id="fb90b-192">e.</span></span> <span data-ttu-id="fb90b-193">In the **Audience(SP Entity ID)** textbox, enter the **Identifier** value, which you have entered in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fb90b-193">In the **Audience(SP Entity ID)** textbox, enter the **Identifier** value, which you have entered in the Azure portal.</span></span>

    <span data-ttu-id="fb90b-194">f.</span><span class="sxs-lookup"><span data-stu-id="fb90b-194">f.</span></span> <span data-ttu-id="fb90b-195">In the **Identity Provider SSO Target URL** textbox, paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fb90b-195">In the **Identity Provider SSO Target URL** textbox, paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="fb90b-196">g.</span><span class="sxs-lookup"><span data-stu-id="fb90b-196">g.</span></span> <span data-ttu-id="fb90b-197">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="fb90b-197">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="fb90b-198">h.</span><span class="sxs-lookup"><span data-stu-id="fb90b-198">h.</span></span> <span data-ttu-id="fb90b-199">In **Name identifier Format** textbox, enter the value `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`.</span><span class="sxs-lookup"><span data-stu-id="fb90b-199">In **Name identifier Format** textbox, enter the value `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`.</span></span>

    <span data-ttu-id="fb90b-200">i.</span><span class="sxs-lookup"><span data-stu-id="fb90b-200">i.</span></span> <span data-ttu-id="fb90b-201">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="fb90b-201">Click **Save**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fb90b-202">Once the content saved, the field will appear blank for security, but the value has been saved in the configuration.</span><span class="sxs-lookup"><span data-stu-id="fb90b-202">Once the content saved, the field will appear blank for security, but the value has been saved in the configuration.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fb90b-203">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="fb90b-203">Create an Azure AD test user</span></span>

<span data-ttu-id="fb90b-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fb90b-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="fb90b-206">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fb90b-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fb90b-207">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="fb90b-207">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/fluxxlabs-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="fb90b-209">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="fb90b-209">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/fluxxlabs-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="fb90b-211">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="fb90b-211">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/fluxxlabs-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="fb90b-213">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fb90b-213">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/fluxxlabs-tutorial/create_aaduser_04.png)

    <span data-ttu-id="fb90b-215">a.</span><span class="sxs-lookup"><span data-stu-id="fb90b-215">a.</span></span> <span data-ttu-id="fb90b-216">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fb90b-216">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fb90b-217">b.</span><span class="sxs-lookup"><span data-stu-id="fb90b-217">b.</span></span> <span data-ttu-id="fb90b-218">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fb90b-218">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="fb90b-219">c.</span><span class="sxs-lookup"><span data-stu-id="fb90b-219">c.</span></span> <span data-ttu-id="fb90b-220">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="fb90b-220">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="fb90b-221">d.</span><span class="sxs-lookup"><span data-stu-id="fb90b-221">d.</span></span> <span data-ttu-id="fb90b-222">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="fb90b-222">Click **Create**.</span></span>
  
### <a name="create-a-fluxx-labs-test-user"></a><span data-ttu-id="fb90b-223">Create a Fluxx Labs test user</span><span class="sxs-lookup"><span data-stu-id="fb90b-223">Create a Fluxx Labs test user</span></span>

<span data-ttu-id="fb90b-224">To enable Azure AD users to log in to Fluxx Labs, they must be provisioned into Fluxx Labs.</span><span class="sxs-lookup"><span data-stu-id="fb90b-224">To enable Azure AD users to log in to Fluxx Labs, they must be provisioned into Fluxx Labs.</span></span> <span data-ttu-id="fb90b-225">In the case of Fluxx Labs, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="fb90b-225">In the case of Fluxx Labs, provisioning is a manual task.</span></span>

<span data-ttu-id="fb90b-226">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fb90b-226">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="fb90b-227">Log in to your Fluxx Labs company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="fb90b-227">Log in to your Fluxx Labs company site as an administrator.</span></span>

1. <span data-ttu-id="fb90b-228">Click on the  below displayed **icon**.</span><span class="sxs-lookup"><span data-stu-id="fb90b-228">Click on the  below displayed **icon**.</span></span>

    ![Fluxx Labs Configuration](./media/fluxxlabs-tutorial/config6.png)

1. <span data-ttu-id="fb90b-230">On the dashboard, click on the below displayed icon to open the **New PEOPLE** card.</span><span class="sxs-lookup"><span data-stu-id="fb90b-230">On the dashboard, click on the below displayed icon to open the **New PEOPLE** card.</span></span>

    ![Fluxx Labs Configuration](./media/fluxxlabs-tutorial/config4.png)

1. <span data-ttu-id="fb90b-232">On the **NEW PEOPLE** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="fb90b-232">On the **NEW PEOPLE** section, perform the following steps:</span></span>

    ![Fluxx Labs Configuration](./media/fluxxlabs-tutorial/config5.png)

    <span data-ttu-id="fb90b-234">a.</span><span class="sxs-lookup"><span data-stu-id="fb90b-234">a.</span></span> <span data-ttu-id="fb90b-235">Fluxx Labs use email as the unique identifier for SSO logins.</span><span class="sxs-lookup"><span data-stu-id="fb90b-235">Fluxx Labs use email as the unique identifier for SSO logins.</span></span> <span data-ttu-id="fb90b-236">Populate the **SSO UID** field with the user’s email address, that matches the email address, which they are using as login with SSO.</span><span class="sxs-lookup"><span data-stu-id="fb90b-236">Populate the **SSO UID** field with the user’s email address, that matches the email address, which they are using as login with SSO.</span></span>

    <span data-ttu-id="fb90b-237">b.</span><span class="sxs-lookup"><span data-stu-id="fb90b-237">b.</span></span> <span data-ttu-id="fb90b-238">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="fb90b-238">Click **Save**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="fb90b-239">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="fb90b-239">Assign the Azure AD test user</span></span>

<span data-ttu-id="fb90b-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Fluxx Labs.</span><span class="sxs-lookup"><span data-stu-id="fb90b-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Fluxx Labs.</span></span>

![Assign the user role][200]

<span data-ttu-id="fb90b-242">**To assign Britta Simon to Fluxx Labs, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="fb90b-242">**To assign Britta Simon to Fluxx Labs, perform the following steps:**</span></span>

1. <span data-ttu-id="fb90b-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="fb90b-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="fb90b-245">In the applications list, select **Fluxx Labs**.</span><span class="sxs-lookup"><span data-stu-id="fb90b-245">In the applications list, select **Fluxx Labs**.</span></span>

    ![The Fluxx Labs link in the Applications list](./media/fluxxlabs-tutorial/tutorial_fluxxlabs_app.png)  

1. <span data-ttu-id="fb90b-247">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="fb90b-247">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="fb90b-249">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="fb90b-249">Click **Add** button.</span></span> <span data-ttu-id="fb90b-250">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="fb90b-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="fb90b-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="fb90b-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="fb90b-253">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="fb90b-253">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="fb90b-254">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="fb90b-254">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="fb90b-255">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="fb90b-255">Test single sign-on</span></span>

<span data-ttu-id="fb90b-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="fb90b-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fb90b-257">When you click the Fluxx Labs tile in the Access Panel, you should get automatically signed-on to your Fluxx Labs application.</span><span class="sxs-lookup"><span data-stu-id="fb90b-257">When you click the Fluxx Labs tile in the Access Panel, you should get automatically signed-on to your Fluxx Labs application.</span></span>
<span data-ttu-id="fb90b-258">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fb90b-258">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fb90b-259">Additional resources</span><span class="sxs-lookup"><span data-stu-id="fb90b-259">Additional resources</span></span>

* [<span data-ttu-id="fb90b-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb90b-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="fb90b-261">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fb90b-261">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/fluxxlabs-tutorial/tutorial_general_01.png
[2]: ./media/fluxxlabs-tutorial/tutorial_general_02.png
[3]: ./media/fluxxlabs-tutorial/tutorial_general_03.png
[4]: ./media/fluxxlabs-tutorial/tutorial_general_04.png

[100]: ./media/fluxxlabs-tutorial/tutorial_general_100.png

[200]: ./media/fluxxlabs-tutorial/tutorial_general_200.png
[201]: ./media/fluxxlabs-tutorial/tutorial_general_201.png
[202]: ./media/fluxxlabs-tutorial/tutorial_general_202.png
[203]: ./media/fluxxlabs-tutorial/tutorial_general_203.png
