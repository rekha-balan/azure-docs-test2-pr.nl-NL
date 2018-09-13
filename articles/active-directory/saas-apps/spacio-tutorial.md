---
title: 'Tutorial: Azure Active Directory integration with Spacio | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Spacio.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9df8d199-b955-483c-aa4e-cabad1a0b9d6
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/16/2018
ms.author: jeedes
ms.openlocfilehash: aa5c91265a832ef8a66948086b407688fdcbbbc2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869639"
---
# <a name="tutorial-azure-active-directory-integration-with-spacio"></a><span data-ttu-id="26229-103">Tutorial: Azure Active Directory integration with Spacio</span><span class="sxs-lookup"><span data-stu-id="26229-103">Tutorial: Azure Active Directory integration with Spacio</span></span>

<span data-ttu-id="26229-104">In this tutorial, you learn how to integrate Spacio with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="26229-104">In this tutorial, you learn how to integrate Spacio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="26229-105">Integrating Spacio with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="26229-105">Integrating Spacio with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="26229-106">You can control in Azure AD who has access to Spacio.</span><span class="sxs-lookup"><span data-stu-id="26229-106">You can control in Azure AD who has access to Spacio.</span></span>
- <span data-ttu-id="26229-107">You can enable your users to automatically get signed-on to Spacio (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="26229-107">You can enable your users to automatically get signed-on to Spacio (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="26229-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="26229-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="26229-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="26229-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26229-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="26229-110">Prerequisites</span></span>

<span data-ttu-id="26229-111">To configure Azure AD integration with Spacio, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="26229-111">To configure Azure AD integration with Spacio, you need the following items:</span></span>

- <span data-ttu-id="26229-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="26229-112">An Azure AD subscription</span></span>
- <span data-ttu-id="26229-113">A Spacio single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="26229-113">A Spacio single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="26229-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="26229-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="26229-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="26229-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="26229-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="26229-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="26229-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="26229-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="26229-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="26229-118">Scenario description</span></span>
<span data-ttu-id="26229-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="26229-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="26229-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="26229-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="26229-121">Adding Spacio from the gallery</span><span class="sxs-lookup"><span data-stu-id="26229-121">Adding Spacio from the gallery</span></span>
1. <span data-ttu-id="26229-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="26229-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-spacio-from-the-gallery"></a><span data-ttu-id="26229-123">Adding Spacio from the gallery</span><span class="sxs-lookup"><span data-stu-id="26229-123">Adding Spacio from the gallery</span></span>
<span data-ttu-id="26229-124">To configure the integration of Spacio into Azure AD, you need to add Spacio from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="26229-124">To configure the integration of Spacio into Azure AD, you need to add Spacio from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="26229-125">**To add Spacio from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="26229-125">**To add Spacio from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="26229-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="26229-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="26229-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="26229-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="26229-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="26229-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="26229-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="26229-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="26229-133">In the search box, type **Spacio**, select **Spacio** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="26229-133">In the search box, type **Spacio**, select **Spacio** from result panel then click **Add** button to add the application.</span></span>

    ![Spacio in the results list](./media/spacio-tutorial/tutorial_spacio_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="26229-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="26229-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="26229-136">In this section, you configure and test Azure AD single sign-on with Spacio based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="26229-136">In this section, you configure and test Azure AD single sign-on with Spacio based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="26229-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Spacio is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26229-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Spacio is to a user in Azure AD.</span></span> <span data-ttu-id="26229-138">In other words, a link relationship between an Azure AD user and the related user in Spacio needs to be established.</span><span class="sxs-lookup"><span data-stu-id="26229-138">In other words, a link relationship between an Azure AD user and the related user in Spacio needs to be established.</span></span>

<span data-ttu-id="26229-139">To configure and test Azure AD single sign-on with Spacio, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="26229-139">To configure and test Azure AD single sign-on with Spacio, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="26229-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="26229-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="26229-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="26229-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="26229-142">**[Create a Spacio test user](#create-a-spacio-test-user)** - to have a counterpart of Britta Simon in Spacio that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="26229-142">**[Create a Spacio test user](#create-a-spacio-test-user)** - to have a counterpart of Britta Simon in Spacio that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="26229-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="26229-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="26229-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="26229-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="26229-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="26229-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="26229-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Spacio application.</span><span class="sxs-lookup"><span data-stu-id="26229-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Spacio application.</span></span>

<span data-ttu-id="26229-147">**To configure Azure AD single sign-on with Spacio, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="26229-147">**To configure Azure AD single sign-on with Spacio, perform the following steps:**</span></span>

1. <span data-ttu-id="26229-148">In the Azure portal, on the **Spacio** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="26229-148">In the Azure portal, on the **Spacio** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="26229-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="26229-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/spacio-tutorial/tutorial_spacio_samlbase.png)

1. <span data-ttu-id="26229-152">On the **Spacio Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="26229-152">On the **Spacio Domain and URLs** section, perform the following steps:</span></span>

    ![Spacio Domain and URLs single sign-on information](./media/spacio-tutorial/tutorial_spacio_url.png)

    <span data-ttu-id="26229-154">a.</span><span class="sxs-lookup"><span data-stu-id="26229-154">a.</span></span> <span data-ttu-id="26229-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.spac.io/<brokerageID>`</span><span class="sxs-lookup"><span data-stu-id="26229-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.spac.io/<brokerageID>`</span></span>

    <span data-ttu-id="26229-156">b.</span><span class="sxs-lookup"><span data-stu-id="26229-156">b.</span></span> <span data-ttu-id="26229-157">In the **Identifier** textbox, type a URL using the following pattern: `https://sso.spac.io/<brokerageID>`</span><span class="sxs-lookup"><span data-stu-id="26229-157">In the **Identifier** textbox, type a URL using the following pattern: `https://sso.spac.io/<brokerageID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="26229-158">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="26229-158">These values are not real.</span></span> <span data-ttu-id="26229-159">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="26229-159">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="26229-160">Contact [Spacio Client support team](mailto:support@spac.io) to get these values.</span><span class="sxs-lookup"><span data-stu-id="26229-160">Contact [Spacio Client support team](mailto:support@spac.io) to get these values.</span></span> 

1. <span data-ttu-id="26229-161">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="26229-161">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/spacio-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="26229-163">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="26229-163">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span> 

    ![The Certificate download link](./media/spacio-tutorial/tutorial_spacio_certificate.png)

1. <span data-ttu-id="26229-165">To configure single sign-on on **Spacio** side, you need to send the **App Federation Metadata Url** to [Spacio support team](mailto:support@spac.io).</span><span class="sxs-lookup"><span data-stu-id="26229-165">To configure single sign-on on **Spacio** side, you need to send the **App Federation Metadata Url** to [Spacio support team](mailto:support@spac.io).</span></span> <span data-ttu-id="26229-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="26229-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="26229-167">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="26229-167">Create an Azure AD test user</span></span>

<span data-ttu-id="26229-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="26229-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="26229-170">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="26229-170">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="26229-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="26229-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/spacio-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="26229-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="26229-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/spacio-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="26229-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="26229-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/spacio-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="26229-177">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="26229-177">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/spacio-tutorial/create_aaduser_04.png)

    <span data-ttu-id="26229-179">a.</span><span class="sxs-lookup"><span data-stu-id="26229-179">a.</span></span> <span data-ttu-id="26229-180">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="26229-180">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="26229-181">b.</span><span class="sxs-lookup"><span data-stu-id="26229-181">b.</span></span> <span data-ttu-id="26229-182">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="26229-182">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="26229-183">c.</span><span class="sxs-lookup"><span data-stu-id="26229-183">c.</span></span> <span data-ttu-id="26229-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="26229-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="26229-185">d.</span><span class="sxs-lookup"><span data-stu-id="26229-185">d.</span></span> <span data-ttu-id="26229-186">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="26229-186">Click **Create**.</span></span>
 
### <a name="create-a-spacio-test-user"></a><span data-ttu-id="26229-187">Create a Spacio test user</span><span class="sxs-lookup"><span data-stu-id="26229-187">Create a Spacio test user</span></span>

<span data-ttu-id="26229-188">In this section, you create a user called Britta Simon in Spacio.</span><span class="sxs-lookup"><span data-stu-id="26229-188">In this section, you create a user called Britta Simon in Spacio.</span></span> <span data-ttu-id="26229-189">Work with [Spacio support team](mailto:support@spac.io) to add the users in the Spacio platform.</span><span class="sxs-lookup"><span data-stu-id="26229-189">Work with [Spacio support team](mailto:support@spac.io) to add the users in the Spacio platform.</span></span> <span data-ttu-id="26229-190">Users must be created and activated before you use single sign-on</span><span class="sxs-lookup"><span data-stu-id="26229-190">Users must be created and activated before you use single sign-on</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="26229-191">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="26229-191">Assign the Azure AD test user</span></span>

<span data-ttu-id="26229-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Spacio.</span><span class="sxs-lookup"><span data-stu-id="26229-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Spacio.</span></span>

![Assign the user role][200] 

<span data-ttu-id="26229-194">**To assign Britta Simon to Spacio, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="26229-194">**To assign Britta Simon to Spacio, perform the following steps:**</span></span>

1. <span data-ttu-id="26229-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="26229-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="26229-197">In the applications list, select **Spacio**.</span><span class="sxs-lookup"><span data-stu-id="26229-197">In the applications list, select **Spacio**.</span></span>

    ![The Spacio link in the Applications list](./media/spacio-tutorial/tutorial_spacio_app.png)  

1. <span data-ttu-id="26229-199">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="26229-199">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="26229-201">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="26229-201">Click **Add** button.</span></span> <span data-ttu-id="26229-202">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="26229-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="26229-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="26229-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="26229-205">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="26229-205">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="26229-206">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="26229-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="26229-207">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="26229-207">Test single sign-on</span></span>

<span data-ttu-id="26229-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="26229-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="26229-209">When you click the Spacio tile in the Access Panel, you should get automatically signed-on to your Spacio application.</span><span class="sxs-lookup"><span data-stu-id="26229-209">When you click the Spacio tile in the Access Panel, you should get automatically signed-on to your Spacio application.</span></span>
<span data-ttu-id="26229-210">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="26229-210">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="26229-211">Additional resources</span><span class="sxs-lookup"><span data-stu-id="26229-211">Additional resources</span></span>

* [<span data-ttu-id="26229-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="26229-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="26229-213">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="26229-213">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/spacio-tutorial/tutorial_general_01.png
[2]: ./media/spacio-tutorial/tutorial_general_02.png
[3]: ./media/spacio-tutorial/tutorial_general_03.png
[4]: ./media/spacio-tutorial/tutorial_general_04.png

[100]: ./media/spacio-tutorial/tutorial_general_100.png

[200]: ./media/spacio-tutorial/tutorial_general_200.png
[201]: ./media/spacio-tutorial/tutorial_general_201.png
[202]: ./media/spacio-tutorial/tutorial_general_202.png
[203]: ./media/spacio-tutorial/tutorial_general_203.png

