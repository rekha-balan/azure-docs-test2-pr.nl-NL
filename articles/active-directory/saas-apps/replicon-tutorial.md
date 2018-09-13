---
title: 'Tutorial: Azure Active Directory integration with Replicon | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Replicon.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2018
ms.author: jeedes
ms.openlocfilehash: 7edfe5a115caf4ee6e4677e5fd7f324b8f3873ee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867682"
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a><span data-ttu-id="725db-103">Tutorial: Azure Active Directory integration with Replicon</span><span class="sxs-lookup"><span data-stu-id="725db-103">Tutorial: Azure Active Directory integration with Replicon</span></span>

<span data-ttu-id="725db-104">In this tutorial, you learn how to integrate Replicon with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="725db-104">In this tutorial, you learn how to integrate Replicon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="725db-105">Integrating Replicon with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="725db-105">Integrating Replicon with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="725db-106">You can control in Azure AD who has access to Replicon.</span><span class="sxs-lookup"><span data-stu-id="725db-106">You can control in Azure AD who has access to Replicon.</span></span>
- <span data-ttu-id="725db-107">You can enable your users to automatically get signed-on to Replicon (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="725db-107">You can enable your users to automatically get signed-on to Replicon (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="725db-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="725db-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="725db-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="725db-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="725db-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="725db-110">Prerequisites</span></span>

<span data-ttu-id="725db-111">To configure Azure AD integration with Replicon, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="725db-111">To configure Azure AD integration with Replicon, you need the following items:</span></span>

- <span data-ttu-id="725db-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="725db-112">An Azure AD subscription</span></span>
- <span data-ttu-id="725db-113">A Replicon single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="725db-113">A Replicon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="725db-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="725db-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="725db-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="725db-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="725db-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="725db-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="725db-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="725db-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="725db-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="725db-118">Scenario description</span></span>
<span data-ttu-id="725db-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="725db-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="725db-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="725db-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="725db-121">Adding Replicon from the gallery</span><span class="sxs-lookup"><span data-stu-id="725db-121">Adding Replicon from the gallery</span></span>
2. <span data-ttu-id="725db-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="725db-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-replicon-from-the-gallery"></a><span data-ttu-id="725db-123">Adding Replicon from the gallery</span><span class="sxs-lookup"><span data-stu-id="725db-123">Adding Replicon from the gallery</span></span>
<span data-ttu-id="725db-124">To configure the integration of Replicon into Azure AD, you need to add Replicon from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="725db-124">To configure the integration of Replicon into Azure AD, you need to add Replicon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="725db-125">**To add Replicon from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="725db-125">**To add Replicon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="725db-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="725db-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span>

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="725db-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="725db-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="725db-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="725db-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="725db-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="725db-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="725db-133">In the search box, type **Replicon**, select **Replicon** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="725db-133">In the search box, type **Replicon**, select **Replicon** from result panel then click **Add** button to add the application.</span></span>

    ![Replicon in the results list](./media/replicon-tutorial/tutorial_replicon_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="725db-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="725db-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="725db-136">In this section, you configure and test Azure AD single sign-on with Replicon based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="725db-136">In this section, you configure and test Azure AD single sign-on with Replicon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="725db-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Replicon is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="725db-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Replicon is to a user in Azure AD.</span></span> <span data-ttu-id="725db-138">In other words, a link relationship between an Azure AD user and the related user in Replicon needs to be established.</span><span class="sxs-lookup"><span data-stu-id="725db-138">In other words, a link relationship between an Azure AD user and the related user in Replicon needs to be established.</span></span>

<span data-ttu-id="725db-139">In Replicon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="725db-139">In Replicon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="725db-140">To configure and test Azure AD single sign-on with Replicon, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="725db-140">To configure and test Azure AD single sign-on with Replicon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="725db-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="725db-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="725db-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="725db-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="725db-143">**[Create a Replicon test user](#create-a-replicon-test-user)** - to have a counterpart of Britta Simon in Replicon that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="725db-143">**[Create a Replicon test user](#create-a-replicon-test-user)** - to have a counterpart of Britta Simon in Replicon that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="725db-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="725db-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="725db-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="725db-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="725db-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="725db-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="725db-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Replicon application.</span><span class="sxs-lookup"><span data-stu-id="725db-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Replicon application.</span></span>

<span data-ttu-id="725db-148">**To configure Azure AD single sign-on with Replicon, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="725db-148">**To configure Azure AD single sign-on with Replicon, perform the following steps:**</span></span>

1. <span data-ttu-id="725db-149">In the Azure portal, on the **Replicon** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="725db-149">In the Azure portal, on the **Replicon** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="725db-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="725db-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/replicon-tutorial/tutorial_replicon_samlbase.png)

3. <span data-ttu-id="725db-153">On the **Replicon Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="725db-153">On the **Replicon Domain and URLs** section, perform the following steps:</span></span>

    ![Replicon Domain and URLs single sign-on information](./media/replicon-tutorial/tutorial_replicon_url.png)

    <span data-ttu-id="725db-155">a.</span><span class="sxs-lookup"><span data-stu-id="725db-155">a.</span></span> <span data-ttu-id="725db-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://na2.replicon.com/<companyname>/saml2/sp-sso/post`</span><span class="sxs-lookup"><span data-stu-id="725db-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://na2.replicon.com/<companyname>/saml2/sp-sso/post`</span></span>

    <span data-ttu-id="725db-157">b.</span><span class="sxs-lookup"><span data-stu-id="725db-157">b.</span></span> <span data-ttu-id="725db-158">In the **Identifier** textbox, type a URL using the following pattern: `https://global.replicon.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="725db-158">In the **Identifier** textbox, type a URL using the following pattern: `https://global.replicon.com/<companyname>`</span></span>

    <span data-ttu-id="725db-159">c.</span><span class="sxs-lookup"><span data-stu-id="725db-159">c.</span></span> <span data-ttu-id="725db-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://global.replicon.com/!/saml2/<companyname>/sso/post`</span><span class="sxs-lookup"><span data-stu-id="725db-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://global.replicon.com/!/saml2/<companyname>/sso/post`</span></span>

    > [!NOTE]
    > <span data-ttu-id="725db-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="725db-161">These values are not real.</span></span> <span data-ttu-id="725db-162">Update these values with the actual Sign-On URL, Identifier, and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="725db-162">Update these values with the actual Sign-On URL, Identifier, and Reply URL.</span></span> <span data-ttu-id="725db-163">Contact [Replicon Client support team](https://www.replicon.com/customerzone/contact-support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="725db-163">Contact [Replicon Client support team](https://www.replicon.com/customerzone/contact-support) to get these values.</span></span> 

4. <span data-ttu-id="725db-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="725db-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/replicon-tutorial/tutorial_replicon_certificate.png) 

5. <span data-ttu-id="725db-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="725db-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/replicon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="725db-168">In a different web browser window, log into your Replicon company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="725db-168">In a different web browser window, log into your Replicon company site as an administrator.</span></span>

7. <span data-ttu-id="725db-169">To configure SAML 2.0, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="725db-169">To configure SAML 2.0, perform the following steps:</span></span>

    <span data-ttu-id="725db-170">![Enable SAML authentication](./media/replicon-tutorial/ic777805.png "Enable SAML authentication")</span><span class="sxs-lookup"><span data-stu-id="725db-170">![Enable SAML authentication](./media/replicon-tutorial/ic777805.png "Enable SAML authentication")</span></span>

    <span data-ttu-id="725db-171">a.</span><span class="sxs-lookup"><span data-stu-id="725db-171">a.</span></span> <span data-ttu-id="725db-172">To display the **EnableSAML Authentication2** dialog, append the following to your URL, after your company key: `/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2`</span><span class="sxs-lookup"><span data-stu-id="725db-172">To display the **EnableSAML Authentication2** dialog, append the following to your URL, after your company key: `/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2`</span></span>

    * <span data-ttu-id="725db-173">The following shows the schema of the complete URL: `https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2`</span><span class="sxs-lookup"><span data-stu-id="725db-173">The following shows the schema of the complete URL: `https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2`</span></span>

   <span data-ttu-id="725db-174">b.</span><span class="sxs-lookup"><span data-stu-id="725db-174">b.</span></span> <span data-ttu-id="725db-175">Click the **+** to expand the **v20Configuration** section.</span><span class="sxs-lookup"><span data-stu-id="725db-175">Click the **+** to expand the **v20Configuration** section.</span></span>

   <span data-ttu-id="725db-176">c.</span><span class="sxs-lookup"><span data-stu-id="725db-176">c.</span></span> <span data-ttu-id="725db-177">Click the **+** to expand the **metaDataConfiguration** section.</span><span class="sxs-lookup"><span data-stu-id="725db-177">Click the **+** to expand the **metaDataConfiguration** section.</span></span>

   <span data-ttu-id="725db-178">d.</span><span class="sxs-lookup"><span data-stu-id="725db-178">d.</span></span> <span data-ttu-id="725db-179">Click **Choose File**, to select your identity provider metadata XML file, and click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="725db-179">Click **Choose File**, to select your identity provider metadata XML file, and click **Submit**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="725db-180">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="725db-180">Create an Azure AD test user</span></span>

<span data-ttu-id="725db-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="725db-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="725db-183">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="725db-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="725db-184">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="725db-184">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/replicon-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="725db-186">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="725db-186">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/replicon-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="725db-188">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="725db-188">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/replicon-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="725db-190">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="725db-190">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/replicon-tutorial/create_aaduser_04.png)

    <span data-ttu-id="725db-192">a.</span><span class="sxs-lookup"><span data-stu-id="725db-192">a.</span></span> <span data-ttu-id="725db-193">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="725db-193">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="725db-194">b.</span><span class="sxs-lookup"><span data-stu-id="725db-194">b.</span></span> <span data-ttu-id="725db-195">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="725db-195">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="725db-196">c.</span><span class="sxs-lookup"><span data-stu-id="725db-196">c.</span></span> <span data-ttu-id="725db-197">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="725db-197">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="725db-198">d.</span><span class="sxs-lookup"><span data-stu-id="725db-198">d.</span></span> <span data-ttu-id="725db-199">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="725db-199">Click **Create**.</span></span>

### <a name="create-a-replicon-test-user"></a><span data-ttu-id="725db-200">Create a Replicon test user</span><span class="sxs-lookup"><span data-stu-id="725db-200">Create a Replicon test user</span></span>

<span data-ttu-id="725db-201">The objective of this section is to create a user called Britta Simon in Replicon.</span><span class="sxs-lookup"><span data-stu-id="725db-201">The objective of this section is to create a user called Britta Simon in Replicon.</span></span>

<span data-ttu-id="725db-202">**If you need to create user manually, perform following steps:**</span><span class="sxs-lookup"><span data-stu-id="725db-202">**If you need to create user manually, perform following steps:**</span></span>

1. <span data-ttu-id="725db-203">In a web browser window, log into your Replicon company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="725db-203">In a web browser window, log into your Replicon company site as an administrator.</span></span>

2. <span data-ttu-id="725db-204">Go to **Administration \> Users**.</span><span class="sxs-lookup"><span data-stu-id="725db-204">Go to **Administration \> Users**.</span></span>

    <span data-ttu-id="725db-205">![Users](./media/replicon-tutorial/ic777806.png "Users")</span><span class="sxs-lookup"><span data-stu-id="725db-205">![Users](./media/replicon-tutorial/ic777806.png "Users")</span></span>

3. <span data-ttu-id="725db-206">Click **+Add User**.</span><span class="sxs-lookup"><span data-stu-id="725db-206">Click **+Add User**.</span></span>

    <span data-ttu-id="725db-207">![Add User](./media/replicon-tutorial/ic777807.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="725db-207">![Add User](./media/replicon-tutorial/ic777807.png "Add User")</span></span>

4. <span data-ttu-id="725db-208">In the **User Profile** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="725db-208">In the **User Profile** section, perform the following steps:</span></span>

    <span data-ttu-id="725db-209">![User profile](./media/replicon-tutorial/ic777808.png "User profile")</span><span class="sxs-lookup"><span data-stu-id="725db-209">![User profile](./media/replicon-tutorial/ic777808.png "User profile")</span></span>

    <span data-ttu-id="725db-210">a.</span><span class="sxs-lookup"><span data-stu-id="725db-210">a.</span></span> <span data-ttu-id="725db-211">In the **Login Name** textbox, type the Azure AD email address of the Azure AD user you want to provision like **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="725db-211">In the **Login Name** textbox, type the Azure AD email address of the Azure AD user you want to provision like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="725db-212">b.</span><span class="sxs-lookup"><span data-stu-id="725db-212">b.</span></span> <span data-ttu-id="725db-213">As **Authentication Type**, select **SSO**.</span><span class="sxs-lookup"><span data-stu-id="725db-213">As **Authentication Type**, select **SSO**.</span></span>

    <span data-ttu-id="725db-214">c.</span><span class="sxs-lookup"><span data-stu-id="725db-214">c.</span></span> <span data-ttu-id="725db-215">In the **Department** textbox, type the user’s department.</span><span class="sxs-lookup"><span data-stu-id="725db-215">In the **Department** textbox, type the user’s department.</span></span>

    <span data-ttu-id="725db-216">d.</span><span class="sxs-lookup"><span data-stu-id="725db-216">d.</span></span> <span data-ttu-id="725db-217">As **Employee Type**, select **Administrator**.</span><span class="sxs-lookup"><span data-stu-id="725db-217">As **Employee Type**, select **Administrator**.</span></span>

    <span data-ttu-id="725db-218">e.</span><span class="sxs-lookup"><span data-stu-id="725db-218">e.</span></span> <span data-ttu-id="725db-219">Click **Save User Profile**.</span><span class="sxs-lookup"><span data-stu-id="725db-219">Click **Save User Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="725db-220">You can use any other Replicon user account creation tools or APIs provided by Replicon to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="725db-220">You can use any other Replicon user account creation tools or APIs provided by Replicon to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="725db-221">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="725db-221">Assign the Azure AD test user</span></span>

<span data-ttu-id="725db-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Replicon.</span><span class="sxs-lookup"><span data-stu-id="725db-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Replicon.</span></span>

![Assign the user role][200]

<span data-ttu-id="725db-224">**To assign Britta Simon to Replicon, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="725db-224">**To assign Britta Simon to Replicon, perform the following steps:**</span></span>

1. <span data-ttu-id="725db-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="725db-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="725db-227">In the applications list, select **Replicon**.</span><span class="sxs-lookup"><span data-stu-id="725db-227">In the applications list, select **Replicon**.</span></span>

    ![The Replicon link in the Applications list](./media/replicon-tutorial/tutorial_replicon_app.png)

3. <span data-ttu-id="725db-229">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="725db-229">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="725db-231">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="725db-231">Click **Add** button.</span></span> <span data-ttu-id="725db-232">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="725db-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="725db-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="725db-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="725db-235">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="725db-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="725db-236">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="725db-236">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="725db-237">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="725db-237">Test single sign-on</span></span>

<span data-ttu-id="725db-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="725db-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="725db-239">When you click the Replicon tile in the Access Panel, you should get automatically signed-on to your Replicon application.</span><span class="sxs-lookup"><span data-stu-id="725db-239">When you click the Replicon tile in the Access Panel, you should get automatically signed-on to your Replicon application.</span></span>
<span data-ttu-id="725db-240">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="725db-240">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="725db-241">Additional resources</span><span class="sxs-lookup"><span data-stu-id="725db-241">Additional resources</span></span>

* [<span data-ttu-id="725db-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="725db-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="725db-243">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="725db-243">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/replicon-tutorial/tutorial_general_01.png
[2]: ./media/replicon-tutorial/tutorial_general_02.png
[3]: ./media/replicon-tutorial/tutorial_general_03.png
[4]: ./media/replicon-tutorial/tutorial_general_04.png

[100]: ./media/replicon-tutorial/tutorial_general_100.png

[200]: ./media/replicon-tutorial/tutorial_general_200.png
[201]: ./media/replicon-tutorial/tutorial_general_201.png
[202]: ./media/replicon-tutorial/tutorial_general_202.png
[203]: ./media/replicon-tutorial/tutorial_general_203.png
