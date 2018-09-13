---
title: 'Tutorial: Azure Active Directory integration with GitHub | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and GitHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8761f5ca-c57c-4a7e-bf14-ac0421bd3b5e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2018
ms.author: jeedes
ms.openlocfilehash: b2a90a4599e5d07baba721d5649b72422dc5cb4d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864324"
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a><span data-ttu-id="dc2d8-103">Tutorial: Azure Active Directory integration with GitHub</span><span class="sxs-lookup"><span data-stu-id="dc2d8-103">Tutorial: Azure Active Directory integration with GitHub</span></span>

<span data-ttu-id="dc2d8-104">In this tutorial, you learn how to integrate GitHub with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dc2d8-104">In this tutorial, you learn how to integrate GitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dc2d8-105">Integrating GitHub with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="dc2d8-105">Integrating GitHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dc2d8-106">You can control in Azure AD who has access to GitHub.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-106">You can control in Azure AD who has access to GitHub.</span></span>
- <span data-ttu-id="dc2d8-107">You can enable your users to automatically get signed-on to GitHub (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-107">You can enable your users to automatically get signed-on to GitHub (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="dc2d8-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="dc2d8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="dc2d8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc2d8-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dc2d8-110">Prerequisites</span></span>

<span data-ttu-id="dc2d8-111">To configure Azure AD integration with GitHub, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="dc2d8-111">To configure Azure AD integration with GitHub, you need the following items:</span></span>

- <span data-ttu-id="dc2d8-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="dc2d8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dc2d8-113">A GitHub single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="dc2d8-113">A GitHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dc2d8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dc2d8-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="dc2d8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dc2d8-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dc2d8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dc2d8-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dc2d8-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="dc2d8-118">Scenario description</span></span>

<span data-ttu-id="dc2d8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dc2d8-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="dc2d8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dc2d8-121">Adding GitHub from the gallery</span><span class="sxs-lookup"><span data-stu-id="dc2d8-121">Adding GitHub from the gallery</span></span>
2. <span data-ttu-id="dc2d8-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dc2d8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-github-from-the-gallery"></a><span data-ttu-id="dc2d8-123">Adding GitHub from the gallery</span><span class="sxs-lookup"><span data-stu-id="dc2d8-123">Adding GitHub from the gallery</span></span>

<span data-ttu-id="dc2d8-124">To configure the integration of GitHub into Azure AD, you need to add GitHub from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-124">To configure the integration of GitHub into Azure AD, you need to add GitHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dc2d8-125">**To add GitHub from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dc2d8-125">**To add GitHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dc2d8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="dc2d8-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dc2d8-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="dc2d8-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="dc2d8-133">In the search box, type **GitHub**, select **GitHub** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-133">In the search box, type **GitHub**, select **GitHub** from result panel then click **Add** button to add the application.</span></span>

    ![GitHub in the results list](./media/github-tutorial/tutorial_github_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="dc2d8-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dc2d8-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="dc2d8-136">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dc2d8-136">In this section, you configure and test Azure AD single sign-on with GitHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dc2d8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in GitHub is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-137">For single sign-on to work, Azure AD needs to know what the counterpart user in GitHub is to a user in Azure AD.</span></span> <span data-ttu-id="dc2d8-138">In other words, a link relationship between an Azure AD user and the related user in GitHub needs to be established.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-138">In other words, a link relationship between an Azure AD user and the related user in GitHub needs to be established.</span></span>

<span data-ttu-id="dc2d8-139">To configure and test Azure AD single sign-on with GitHub, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="dc2d8-139">To configure and test Azure AD single sign-on with GitHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dc2d8-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dc2d8-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dc2d8-142">**[Create a GitHub test user](#create-a-github-test-user)** - to have a counterpart of Britta Simon in GitHub that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-142">**[Create a GitHub test user](#create-a-github-test-user)** - to have a counterpart of Britta Simon in GitHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dc2d8-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dc2d8-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="dc2d8-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dc2d8-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="dc2d8-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your GitHub application.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your GitHub application.</span></span>

<span data-ttu-id="dc2d8-147">**To configure Azure AD single sign-on with GitHub, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dc2d8-147">**To configure Azure AD single sign-on with GitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="dc2d8-148">In the Azure portal, on the **GitHub** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-148">In the Azure portal, on the **GitHub** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="dc2d8-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/github-tutorial/tutorial_github_samlbase.png)

3. <span data-ttu-id="dc2d8-152">On the **GitHub Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dc2d8-152">On the **GitHub Domain and URLs** section, perform the following steps:</span></span>

    ![GitHub Domain and URLs single sign-on information](./media/github-tutorial/tutorial_github_url.png)

    <span data-ttu-id="dc2d8-154">a.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-154">a.</span></span> <span data-ttu-id="dc2d8-155">In the **Sign on URL** textbox, type a URL using the following pattern: `https://github.com/orgs/<entity-id>/sso`</span><span class="sxs-lookup"><span data-stu-id="dc2d8-155">In the **Sign on URL** textbox, type a URL using the following pattern: `https://github.com/orgs/<entity-id>/sso`</span></span>

    <span data-ttu-id="dc2d8-156">b.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-156">b.</span></span> <span data-ttu-id="dc2d8-157">In the **Identifier (Entity ID)** textbox, type a URL using the following pattern: `https://github.com/orgs/<entity-id>`</span><span class="sxs-lookup"><span data-stu-id="dc2d8-157">In the **Identifier (Entity ID)** textbox, type a URL using the following pattern: `https://github.com/orgs/<entity-id>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="dc2d8-158">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-158">Please note that these are not the real values.</span></span> <span data-ttu-id="dc2d8-159">You have to update these values with the actual Sign on URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-159">You have to update these values with the actual Sign on URL and Identifier.</span></span> <span data-ttu-id="dc2d8-160">Here we suggest you to use the unique value of string in the Identifier.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-160">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="dc2d8-161">Go to GitHub Admin section to retrieve these values.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-161">Go to GitHub Admin section to retrieve these values.</span></span>

4. <span data-ttu-id="dc2d8-162">On the **User Attributes** section, select **User Identifier** as user.mail.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-162">On the **User Attributes** section, select **User Identifier** as user.mail.</span></span>

    ![Configure Single Sign-On](./media/github-tutorial/tutorial_github_attribute_new01.png)

5. <span data-ttu-id="dc2d8-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/github-tutorial/tutorial_github_certificate.png) 

6. <span data-ttu-id="dc2d8-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/github-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="dc2d8-168">On the **GitHub Configuration** section, click **Configure GitHub** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-168">On the **GitHub Configuration** section, click **Configure GitHub** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dc2d8-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="dc2d8-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![GitHub Configuration](./media/github-tutorial/tutorial_github_configure.png) 

8. <span data-ttu-id="dc2d8-171">In a different web browser window, log into your GitHub organization site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-171">In a different web browser window, log into your GitHub organization site as an administrator.</span></span>

9. <span data-ttu-id="dc2d8-172">Navigate to **Settings** and click **Security**</span><span class="sxs-lookup"><span data-stu-id="dc2d8-172">Navigate to **Settings** and click **Security**</span></span>

    ![Settings](./media/github-tutorial/tutorial_github_config_github_03.png)

10. <span data-ttu-id="dc2d8-174">Check the **Enable SAML authentication** box, revealing the Single Sign-on configuration fields.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-174">Check the **Enable SAML authentication** box, revealing the Single Sign-on configuration fields.</span></span> <span data-ttu-id="dc2d8-175">Then, use the single sign-on URL value to update the Single sign-on URL on Azure AD configuration.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-175">Then, use the single sign-on URL value to update the Single sign-on URL on Azure AD configuration.</span></span>

    ![Settings](./media/github-tutorial/tutorial_github_config_github_13.png)

11. <span data-ttu-id="dc2d8-177">Configure the following fields:</span><span class="sxs-lookup"><span data-stu-id="dc2d8-177">Configure the following fields:</span></span>

    <span data-ttu-id="dc2d8-178">a.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-178">a.</span></span> <span data-ttu-id="dc2d8-179">In the **Sign on URL** textbox, paste **SAML Single sign-on Service URL** value which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-179">In the **Sign on URL** textbox, paste **SAML Single sign-on Service URL** value which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="dc2d8-180">b.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-180">b.</span></span> <span data-ttu-id="dc2d8-181">In the **Issuer** textbox, paste **SAML Entity ID** value which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-181">In the **Issuer** textbox, paste **SAML Entity ID** value which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="dc2d8-182">c.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-182">c.</span></span> <span data-ttu-id="dc2d8-183">Open the downloaded certificate from Azure portal in notepad, paste the content into the **Public Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-183">Open the downloaded certificate from Azure portal in notepad, paste the content into the **Public Certificate** textbox.</span></span>

    ![Settings](./media/github-tutorial/tutorial_github_config_github_051.png)

12. <span data-ttu-id="dc2d8-185">Click on **Test SAML configuration** to confirm that no validation failures or errors during SSO.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-185">Click on **Test SAML configuration** to confirm that no validation failures or errors during SSO.</span></span>

    ![Settings](./media/github-tutorial/tutorial_github_config_github_06.png)

13. <span data-ttu-id="dc2d8-187">Click **Save**</span><span class="sxs-lookup"><span data-stu-id="dc2d8-187">Click **Save**</span></span>

> [!NOTE]
> <span data-ttu-id="dc2d8-188">Single sign-on in GitHub authenticates to a specific organization in GitHub and does not replace the authentication of GitHub itself.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-188">Single sign-on in GitHub authenticates to a specific organization in GitHub and does not replace the authentication of GitHub itself.</span></span> <span data-ttu-id="dc2d8-189">Therefore, if the user's GitHub.com session has expired, you may be asked to authenticate with GitHub's ID/password during the single sign-on process.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-189">Therefore, if the user's GitHub.com session has expired, you may be asked to authenticate with GitHub's ID/password during the single sign-on process.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="dc2d8-190">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="dc2d8-190">Create an Azure AD test user</span></span>

<span data-ttu-id="dc2d8-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="dc2d8-193">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dc2d8-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dc2d8-194">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-194">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/github-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="dc2d8-196">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-196">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/github-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="dc2d8-198">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-198">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/github-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="dc2d8-200">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dc2d8-200">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/github-tutorial/create_aaduser_04.png)

    <span data-ttu-id="dc2d8-202">a.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-202">a.</span></span> <span data-ttu-id="dc2d8-203">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-203">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dc2d8-204">b.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-204">b.</span></span> <span data-ttu-id="dc2d8-205">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-205">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="dc2d8-206">c.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-206">c.</span></span> <span data-ttu-id="dc2d8-207">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-207">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="dc2d8-208">d.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-208">d.</span></span> <span data-ttu-id="dc2d8-209">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-209">Click **Create**.</span></span>

### <a name="create-a-github-test-user"></a><span data-ttu-id="dc2d8-210">Create a GitHub test user</span><span class="sxs-lookup"><span data-stu-id="dc2d8-210">Create a GitHub test user</span></span>

<span data-ttu-id="dc2d8-211">The objective of this section is to create a user called Britta Simon in GitHub.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-211">The objective of this section is to create a user called Britta Simon in GitHub.</span></span> <span data-ttu-id="dc2d8-212">GitHub supports automatic user provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-212">GitHub supports automatic user provisioning, which is by default enabled.</span></span> <span data-ttu-id="dc2d8-213">You can find more details [here](github-provisioning-tutorial.md) on how to configure automatic user provisioning.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-213">You can find more details [here](github-provisioning-tutorial.md) on how to configure automatic user provisioning.</span></span>

<span data-ttu-id="dc2d8-214">**If you need to create user manually, perform following steps:**</span><span class="sxs-lookup"><span data-stu-id="dc2d8-214">**If you need to create user manually, perform following steps:**</span></span>

1. <span data-ttu-id="dc2d8-215">Log in to your GitHub company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-215">Log in to your GitHub company site as an administrator.</span></span>

2. <span data-ttu-id="dc2d8-216">Click **People**.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-216">Click **People**.</span></span>

    <span data-ttu-id="dc2d8-217">![People](./media/github-tutorial/tutorial_github_config_github_08.png "People")</span><span class="sxs-lookup"><span data-stu-id="dc2d8-217">![People](./media/github-tutorial/tutorial_github_config_github_08.png "People")</span></span>

3. <span data-ttu-id="dc2d8-218">Click **Invite member**.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-218">Click **Invite member**.</span></span>

    <span data-ttu-id="dc2d8-219">![Invite Users](./media/github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span><span class="sxs-lookup"><span data-stu-id="dc2d8-219">![Invite Users](./media/github-tutorial/tutorial_github_config_github_09.png "Invite Users")</span></span>

4. <span data-ttu-id="dc2d8-220">On the **Invite member** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dc2d8-220">On the **Invite member** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="dc2d8-221">a.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-221">a.</span></span> <span data-ttu-id="dc2d8-222">In the **Email** textbox, type the email address of Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-222">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="dc2d8-223">![Invite People](./media/github-tutorial/tutorial_github_config_github_10.png "Invite People")</span><span class="sxs-lookup"><span data-stu-id="dc2d8-223">![Invite People](./media/github-tutorial/tutorial_github_config_github_10.png "Invite People")</span></span>

    <span data-ttu-id="dc2d8-224">b.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-224">b.</span></span> <span data-ttu-id="dc2d8-225">Click **Send Invitation**.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-225">Click **Send Invitation**.</span></span>

    <span data-ttu-id="dc2d8-226">![Invite People](./media/github-tutorial/tutorial_github_config_github_11.png "Invite People")</span><span class="sxs-lookup"><span data-stu-id="dc2d8-226">![Invite People](./media/github-tutorial/tutorial_github_config_github_11.png "Invite People")</span></span>

    > [!NOTE]
    > <span data-ttu-id="dc2d8-227">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-227">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="dc2d8-228">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="dc2d8-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="dc2d8-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to GitHub.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to GitHub.</span></span>

![Assign the user role][200] 

<span data-ttu-id="dc2d8-231">**To assign Britta Simon to GitHub, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dc2d8-231">**To assign Britta Simon to GitHub, perform the following steps:**</span></span>

1. <span data-ttu-id="dc2d8-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="dc2d8-234">In the applications list, select **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-234">In the applications list, select **GitHub**.</span></span>

    ![The GitHub link in the Applications list](./media/github-tutorial/tutorial_github_app.png)  

3. <span data-ttu-id="dc2d8-236">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-236">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="dc2d8-238">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-238">Click **Add** button.</span></span> <span data-ttu-id="dc2d8-239">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="dc2d8-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dc2d8-242">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dc2d8-243">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-243">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="dc2d8-244">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="dc2d8-244">Test single sign-on</span></span>

<span data-ttu-id="dc2d8-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dc2d8-246">When you click the GitHub tile in the Access Panel, you should get automatically signed-on to your GitHub application.</span><span class="sxs-lookup"><span data-stu-id="dc2d8-246">When you click the GitHub tile in the Access Panel, you should get automatically signed-on to your GitHub application.</span></span>
<span data-ttu-id="dc2d8-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dc2d8-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dc2d8-248">Additional resources</span><span class="sxs-lookup"><span data-stu-id="dc2d8-248">Additional resources</span></span>

* [<span data-ttu-id="dc2d8-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc2d8-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="dc2d8-250">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dc2d8-250">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/github-tutorial/tutorial_general_01.png
[2]: ./media/github-tutorial/tutorial_general_02.png
[3]: ./media/github-tutorial/tutorial_general_03.png
[4]: ./media/github-tutorial/tutorial_general_04.png

[100]: ./media/github-tutorial/tutorial_general_100.png

[200]: ./media/github-tutorial/tutorial_general_200.png
[201]: ./media/github-tutorial/tutorial_general_201.png
[202]: ./media/github-tutorial/tutorial_general_202.png
[203]: ./media/github-tutorial/tutorial_general_203.png