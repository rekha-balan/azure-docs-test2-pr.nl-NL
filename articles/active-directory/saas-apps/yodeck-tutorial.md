---
title: 'Tutorial: Azure Active Directory integration with Yodeck | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Yodeck.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b2c8dccb-eeb0-4f4d-a24d-8320631ce819
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2018
ms.author: jeedes
ms.openlocfilehash: b017efd2c170f543041dcb35a3a3d040389d1dac
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865159"
---
# <a name="tutorial-azure-active-directory-integration-with-yodeck"></a><span data-ttu-id="077ea-103">Tutorial: Azure Active Directory integration with Yodeck</span><span class="sxs-lookup"><span data-stu-id="077ea-103">Tutorial: Azure Active Directory integration with Yodeck</span></span>

<span data-ttu-id="077ea-104">In this tutorial, you learn how to integrate Yodeck with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="077ea-104">In this tutorial, you learn how to integrate Yodeck with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="077ea-105">Integrating Yodeck with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="077ea-105">Integrating Yodeck with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="077ea-106">You can control in Azure AD who has access to Yodeck.</span><span class="sxs-lookup"><span data-stu-id="077ea-106">You can control in Azure AD who has access to Yodeck.</span></span>
- <span data-ttu-id="077ea-107">You can enable your users to automatically get signed-on to Yodeck (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="077ea-107">You can enable your users to automatically get signed-on to Yodeck (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="077ea-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="077ea-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="077ea-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="077ea-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="077ea-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="077ea-110">Prerequisites</span></span>

<span data-ttu-id="077ea-111">To configure Azure AD integration with Yodeck, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="077ea-111">To configure Azure AD integration with Yodeck, you need the following items:</span></span>

- <span data-ttu-id="077ea-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="077ea-112">An Azure AD subscription</span></span>
- <span data-ttu-id="077ea-113">A Yodeck single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="077ea-113">A Yodeck single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="077ea-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="077ea-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="077ea-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="077ea-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="077ea-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="077ea-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="077ea-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="077ea-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="077ea-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="077ea-118">Scenario description</span></span>
<span data-ttu-id="077ea-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="077ea-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="077ea-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="077ea-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="077ea-121">Adding Yodeck from the gallery</span><span class="sxs-lookup"><span data-stu-id="077ea-121">Adding Yodeck from the gallery</span></span>
1. <span data-ttu-id="077ea-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="077ea-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-yodeck-from-the-gallery"></a><span data-ttu-id="077ea-123">Adding Yodeck from the gallery</span><span class="sxs-lookup"><span data-stu-id="077ea-123">Adding Yodeck from the gallery</span></span>
<span data-ttu-id="077ea-124">To configure the integration of Yodeck into Azure AD, you need to add Yodeck from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="077ea-124">To configure the integration of Yodeck into Azure AD, you need to add Yodeck from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="077ea-125">**To add Yodeck from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="077ea-125">**To add Yodeck from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="077ea-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="077ea-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="077ea-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="077ea-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="077ea-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="077ea-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="077ea-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="077ea-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="077ea-133">In the search box, type **Yodeck**, select **Yodeck** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="077ea-133">In the search box, type **Yodeck**, select **Yodeck** from result panel then click **Add** button to add the application.</span></span>

    ![Yodeck in the results list](./media/yodeck-tutorial/tutorial_yodeck_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="077ea-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="077ea-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="077ea-136">In this section, you configure and test Azure AD single sign-on with Yodeck based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="077ea-136">In this section, you configure and test Azure AD single sign-on with Yodeck based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="077ea-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Yodeck is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="077ea-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Yodeck is to a user in Azure AD.</span></span> <span data-ttu-id="077ea-138">In other words, a link relationship between an Azure AD user and the related user in Yodeck needs to be established.</span><span class="sxs-lookup"><span data-stu-id="077ea-138">In other words, a link relationship between an Azure AD user and the related user in Yodeck needs to be established.</span></span>

<span data-ttu-id="077ea-139">To configure and test Azure AD single sign-on with Yodeck, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="077ea-139">To configure and test Azure AD single sign-on with Yodeck, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="077ea-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="077ea-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="077ea-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="077ea-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="077ea-142">**[Create a Yodeck test user](#create-a-yodeck-test-user)** - to have a counterpart of Britta Simon in Yodeck that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="077ea-142">**[Create a Yodeck test user](#create-a-yodeck-test-user)** - to have a counterpart of Britta Simon in Yodeck that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="077ea-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="077ea-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="077ea-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="077ea-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="077ea-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="077ea-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="077ea-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Yodeck application.</span><span class="sxs-lookup"><span data-stu-id="077ea-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Yodeck application.</span></span>

<span data-ttu-id="077ea-147">**To configure Azure AD single sign-on with Yodeck, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="077ea-147">**To configure Azure AD single sign-on with Yodeck, perform the following steps:**</span></span>

1. <span data-ttu-id="077ea-148">In the Azure portal, on the **Yodeck** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="077ea-148">In the Azure portal, on the **Yodeck** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="077ea-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="077ea-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/yodeck-tutorial/tutorial_yodeck_samlbase.png)

1. <span data-ttu-id="077ea-152">On the **Yodeck Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="077ea-152">On the **Yodeck Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Yodeck Domain and URLs single sign-on information](./media/yodeck-tutorial/tutorial_yodeck_url.png)

    <span data-ttu-id="077ea-154">In the **Identifier (Entity ID)** textbox, type the URL: `https://app.yodeck.com/api/v1/account/metadata/`</span><span class="sxs-lookup"><span data-stu-id="077ea-154">In the **Identifier (Entity ID)** textbox, type the URL: `https://app.yodeck.com/api/v1/account/metadata/`</span></span>

1. <span data-ttu-id="077ea-155">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="077ea-155">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Yodeck Domain and URLs single sign-on information](./media/yodeck-tutorial/tutorial_yodeck_url1.png)

    <span data-ttu-id="077ea-157">In the **Sign-on URL** textbox, type the URL: `https://app.yodeck.com/login`</span><span class="sxs-lookup"><span data-stu-id="077ea-157">In the **Sign-on URL** textbox, type the URL: `https://app.yodeck.com/login`</span></span>

1. <span data-ttu-id="077ea-158">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="077ea-158">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>

    ![The Certificate download link](./media/yodeck-tutorial/tutorial_yodeck_certificate.png)

1. <span data-ttu-id="077ea-160">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="077ea-160">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/yodeck-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="077ea-162">In a different web browser window, log in to your Yodeck company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="077ea-162">In a different web browser window, log in to your Yodeck company site as an administrator.</span></span>

1. <span data-ttu-id="077ea-163">Click on **User Settings** option form the top right corner of the page and select **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="077ea-163">Click on **User Settings** option form the top right corner of the page and select **Account Settings**.</span></span>

    ![Yodeck Configuration](./media/yodeck-tutorial/configure1.png)

1. <span data-ttu-id="077ea-165">Select **SAML** and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="077ea-165">Select **SAML** and perform the following steps:</span></span>

    ![Yodeck Configuration](./media/yodeck-tutorial/configure2.png)

    <span data-ttu-id="077ea-167">a.</span><span class="sxs-lookup"><span data-stu-id="077ea-167">a.</span></span> <span data-ttu-id="077ea-168">Select **Import from URL**.</span><span class="sxs-lookup"><span data-stu-id="077ea-168">Select **Import from URL**.</span></span>

    <span data-ttu-id="077ea-169">b.</span><span class="sxs-lookup"><span data-stu-id="077ea-169">b.</span></span> <span data-ttu-id="077ea-170">In the **URL** textbox, paste the **App Federation Metadata Url** value, which you have copied from the Azure portal and click **Import**.</span><span class="sxs-lookup"><span data-stu-id="077ea-170">In the **URL** textbox, paste the **App Federation Metadata Url** value, which you have copied from the Azure portal and click **Import**.</span></span>
    
    <span data-ttu-id="077ea-171">c.</span><span class="sxs-lookup"><span data-stu-id="077ea-171">c.</span></span> <span data-ttu-id="077ea-172">After importing **App Federation Metadata Url**, the remaining fields populate automatically.</span><span class="sxs-lookup"><span data-stu-id="077ea-172">After importing **App Federation Metadata Url**, the remaining fields populate automatically.</span></span>

    <span data-ttu-id="077ea-173">d.</span><span class="sxs-lookup"><span data-stu-id="077ea-173">d.</span></span> <span data-ttu-id="077ea-174">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="077ea-174">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="077ea-175">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="077ea-175">Create an Azure AD test user</span></span>

<span data-ttu-id="077ea-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="077ea-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="077ea-178">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="077ea-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="077ea-179">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="077ea-179">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/yodeck-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="077ea-181">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="077ea-181">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/yodeck-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="077ea-183">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="077ea-183">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/yodeck-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="077ea-185">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="077ea-185">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/yodeck-tutorial/create_aaduser_04.png)

    <span data-ttu-id="077ea-187">a.</span><span class="sxs-lookup"><span data-stu-id="077ea-187">a.</span></span> <span data-ttu-id="077ea-188">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="077ea-188">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="077ea-189">b.</span><span class="sxs-lookup"><span data-stu-id="077ea-189">b.</span></span> <span data-ttu-id="077ea-190">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="077ea-190">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="077ea-191">c.</span><span class="sxs-lookup"><span data-stu-id="077ea-191">c.</span></span> <span data-ttu-id="077ea-192">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="077ea-192">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="077ea-193">d.</span><span class="sxs-lookup"><span data-stu-id="077ea-193">d.</span></span> <span data-ttu-id="077ea-194">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="077ea-194">Click **Create**.</span></span>
 
### <a name="create-a-yodeck-test-user"></a><span data-ttu-id="077ea-195">Create a Yodeck test user</span><span class="sxs-lookup"><span data-stu-id="077ea-195">Create a Yodeck test user</span></span>

<span data-ttu-id="077ea-196">To enable Azure AD users to log in to Yodeck, they must be provisioned into Yodeck.</span><span class="sxs-lookup"><span data-stu-id="077ea-196">To enable Azure AD users to log in to Yodeck, they must be provisioned into Yodeck.</span></span>
<span data-ttu-id="077ea-197">In the case of Yodeck, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="077ea-197">In the case of Yodeck, provisioning is a manual task.</span></span>

<span data-ttu-id="077ea-198">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="077ea-198">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="077ea-199">Log in to your Yodeck company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="077ea-199">Log in to your Yodeck company site as an administrator.</span></span>

1. <span data-ttu-id="077ea-200">Click on **User Settings** option form the top right corner of the page and select **Users**.</span><span class="sxs-lookup"><span data-stu-id="077ea-200">Click on **User Settings** option form the top right corner of the page and select **Users**.</span></span>

    ![Add Employee](./media/yodeck-tutorial/user1.png)

1. <span data-ttu-id="077ea-202">Click on **+User** to open the **User Details** tab.</span><span class="sxs-lookup"><span data-stu-id="077ea-202">Click on **+User** to open the **User Details** tab.</span></span>

    ![Add Employee](./media/yodeck-tutorial/user2.png)

1. <span data-ttu-id="077ea-204">On the **User Details** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="077ea-204">On the **User Details** dialog page, perform the following steps:</span></span>

    ![Add Employee](./media/yodeck-tutorial/user3.png)

    <span data-ttu-id="077ea-206">a.</span><span class="sxs-lookup"><span data-stu-id="077ea-206">a.</span></span> <span data-ttu-id="077ea-207">In the **First Name** textbox, type the first name of the user like **Britta**.</span><span class="sxs-lookup"><span data-stu-id="077ea-207">In the **First Name** textbox, type the first name of the user like **Britta**.</span></span>

    <span data-ttu-id="077ea-208">b.</span><span class="sxs-lookup"><span data-stu-id="077ea-208">b.</span></span> <span data-ttu-id="077ea-209">In the **Last Name** textbox, type the last name of user like **Simon**.</span><span class="sxs-lookup"><span data-stu-id="077ea-209">In the **Last Name** textbox, type the last name of user like **Simon**.</span></span>

    <span data-ttu-id="077ea-210">c.</span><span class="sxs-lookup"><span data-stu-id="077ea-210">c.</span></span> <span data-ttu-id="077ea-211">In the **Email** textbox, type the email address of user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="077ea-211">In the **Email** textbox, type the email address of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="077ea-212">d.</span><span class="sxs-lookup"><span data-stu-id="077ea-212">d.</span></span> <span data-ttu-id="077ea-213">Select appropriate **Account Permissions** option as per your organizational requirement.</span><span class="sxs-lookup"><span data-stu-id="077ea-213">Select appropriate **Account Permissions** option as per your organizational requirement.</span></span>
    
    <span data-ttu-id="077ea-214">e.</span><span class="sxs-lookup"><span data-stu-id="077ea-214">e.</span></span> <span data-ttu-id="077ea-215">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="077ea-215">Click **Save**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="077ea-216">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="077ea-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="077ea-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Yodeck.</span><span class="sxs-lookup"><span data-stu-id="077ea-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Yodeck.</span></span>

![Assign the user role][200]

<span data-ttu-id="077ea-219">**To assign Britta Simon to Yodeck, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="077ea-219">**To assign Britta Simon to Yodeck, perform the following steps:**</span></span>

1. <span data-ttu-id="077ea-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="077ea-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

1. <span data-ttu-id="077ea-222">In the applications list, select **Yodeck**.</span><span class="sxs-lookup"><span data-stu-id="077ea-222">In the applications list, select **Yodeck**.</span></span>

    ![The Yodeck link in the Applications list](./media/yodeck-tutorial/tutorial_yodeck_app.png)  

1. <span data-ttu-id="077ea-224">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="077ea-224">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="077ea-226">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="077ea-226">Click **Add** button.</span></span> <span data-ttu-id="077ea-227">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="077ea-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="077ea-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="077ea-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="077ea-230">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="077ea-230">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="077ea-231">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="077ea-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="077ea-232">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="077ea-232">Test single sign-on</span></span>

<span data-ttu-id="077ea-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="077ea-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="077ea-234">When you click the Yodeck tile in the Access Panel, you should get automatically signed-on to your Yodeck application.</span><span class="sxs-lookup"><span data-stu-id="077ea-234">When you click the Yodeck tile in the Access Panel, you should get automatically signed-on to your Yodeck application.</span></span>
<span data-ttu-id="077ea-235">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="077ea-235">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="077ea-236">Additional resources</span><span class="sxs-lookup"><span data-stu-id="077ea-236">Additional resources</span></span>

* [<span data-ttu-id="077ea-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="077ea-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="077ea-238">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="077ea-238">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/yodeck-tutorial/tutorial_general_01.png
[2]: ./media/yodeck-tutorial/tutorial_general_02.png
[3]: ./media/yodeck-tutorial/tutorial_general_03.png
[4]: ./media/yodeck-tutorial/tutorial_general_04.png

[100]: ./media/yodeck-tutorial/tutorial_general_100.png

[200]: ./media/yodeck-tutorial/tutorial_general_200.png
[201]: ./media/yodeck-tutorial/tutorial_general_201.png
[202]: ./media/yodeck-tutorial/tutorial_general_202.png
[203]: ./media/yodeck-tutorial/tutorial_general_203.png

