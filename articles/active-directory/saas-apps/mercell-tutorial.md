---
title: 'Tutorial: Azure Active Directory integration with Mercell | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Mercell.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bb94c288-2ed4-4683-acde-62474292df29
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: jeedes
ms.openlocfilehash: e2ca2d4f4a93f6c4bbfdacb6f25185cd59586964
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865128"
---
# <a name="tutorial-azure-active-directory-integration-with-mercell"></a><span data-ttu-id="15f96-103">Tutorial: Azure Active Directory integration with Mercell</span><span class="sxs-lookup"><span data-stu-id="15f96-103">Tutorial: Azure Active Directory integration with Mercell</span></span>

<span data-ttu-id="15f96-104">In this tutorial, you learn how to integrate Mercell with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="15f96-104">In this tutorial, you learn how to integrate Mercell with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="15f96-105">Integrating Mercell with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="15f96-105">Integrating Mercell with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="15f96-106">You can control in Azure AD who has access to Mercell.</span><span class="sxs-lookup"><span data-stu-id="15f96-106">You can control in Azure AD who has access to Mercell.</span></span>
- <span data-ttu-id="15f96-107">You can enable your users to automatically get signed-on to Mercell (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="15f96-107">You can enable your users to automatically get signed-on to Mercell (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="15f96-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="15f96-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="15f96-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="15f96-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15f96-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="15f96-110">Prerequisites</span></span>

<span data-ttu-id="15f96-111">To configure Azure AD integration with Mercell, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="15f96-111">To configure Azure AD integration with Mercell, you need the following items:</span></span>

- <span data-ttu-id="15f96-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="15f96-112">An Azure AD subscription</span></span>
- <span data-ttu-id="15f96-113">A Mercell single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="15f96-113">A Mercell single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="15f96-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="15f96-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="15f96-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="15f96-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="15f96-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="15f96-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="15f96-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="15f96-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="15f96-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="15f96-118">Scenario description</span></span>
<span data-ttu-id="15f96-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="15f96-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="15f96-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="15f96-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="15f96-121">Adding Mercell from the gallery</span><span class="sxs-lookup"><span data-stu-id="15f96-121">Adding Mercell from the gallery</span></span>
2. <span data-ttu-id="15f96-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="15f96-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mercell-from-the-gallery"></a><span data-ttu-id="15f96-123">Adding Mercell from the gallery</span><span class="sxs-lookup"><span data-stu-id="15f96-123">Adding Mercell from the gallery</span></span>
<span data-ttu-id="15f96-124">To configure the integration of Mercell into Azure AD, you need to add Mercell from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="15f96-124">To configure the integration of Mercell into Azure AD, you need to add Mercell from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="15f96-125">**To add Mercell from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="15f96-125">**To add Mercell from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="15f96-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="15f96-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="15f96-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="15f96-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="15f96-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="15f96-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="15f96-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="15f96-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="15f96-133">In the search box, type **Mercell**, select **Mercell** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="15f96-133">In the search box, type **Mercell**, select **Mercell** from result panel then click **Add** button to add the application.</span></span>

    ![Mercell in the results list](./media/mercell-tutorial/tutorial_mercell_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="15f96-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="15f96-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="15f96-136">In this section, you configure and test Azure AD single sign-on with Mercell based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="15f96-136">In this section, you configure and test Azure AD single sign-on with Mercell based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="15f96-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Mercell is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="15f96-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Mercell is to a user in Azure AD.</span></span> <span data-ttu-id="15f96-138">In other words, a link relationship between an Azure AD user and the related user in Mercell needs to be established.</span><span class="sxs-lookup"><span data-stu-id="15f96-138">In other words, a link relationship between an Azure AD user and the related user in Mercell needs to be established.</span></span>

<span data-ttu-id="15f96-139">To configure and test Azure AD single sign-on with Mercell, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="15f96-139">To configure and test Azure AD single sign-on with Mercell, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="15f96-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="15f96-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="15f96-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="15f96-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="15f96-142">**[Create a Mercell test user](#create-a-mercell-test-user)** - to have a counterpart of Britta Simon in Mercell that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="15f96-142">**[Create a Mercell test user](#create-a-mercell-test-user)** - to have a counterpart of Britta Simon in Mercell that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="15f96-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="15f96-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="15f96-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="15f96-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="15f96-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="15f96-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="15f96-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mercell application.</span><span class="sxs-lookup"><span data-stu-id="15f96-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mercell application.</span></span>

<span data-ttu-id="15f96-147">**To configure Azure AD single sign-on with Mercell, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="15f96-147">**To configure Azure AD single sign-on with Mercell, perform the following steps:**</span></span>

1. <span data-ttu-id="15f96-148">In the Azure portal, on the **Mercell** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="15f96-148">In the Azure portal, on the **Mercell** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="15f96-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="15f96-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/mercell-tutorial/tutorial_mercell_samlbase.png)

3. <span data-ttu-id="15f96-152">On the **Mercell Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="15f96-152">On the **Mercell Domain and URLs** section, perform the following steps:</span></span>

    ![Mercell Domain and URLs single sign-on information](./media/mercell-tutorial/tutorial_mercell_url.png)

    <span data-ttu-id="15f96-154">In the **Identifier** textbox, type the URL: `https://my.mercell.com/`</span><span class="sxs-lookup"><span data-stu-id="15f96-154">In the **Identifier** textbox, type the URL: `https://my.mercell.com/`</span></span>

4. <span data-ttu-id="15f96-155">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="15f96-155">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>
    
    ![Configure Single Sign-On](./media/mercell-tutorial/tutorial_metadataurl.png)
     
5. <span data-ttu-id="15f96-157">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="15f96-157">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/mercell-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="15f96-159">To configure single sign-on on **Mercell** side, you need to send the generated **App Federation Metadata Url** to [Mercell support team](mailto:webmaster@mercell.com).</span><span class="sxs-lookup"><span data-stu-id="15f96-159">To configure single sign-on on **Mercell** side, you need to send the generated **App Federation Metadata Url** to [Mercell support team](mailto:webmaster@mercell.com).</span></span> <span data-ttu-id="15f96-160">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="15f96-160">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="15f96-161">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="15f96-161">Create an Azure AD test user</span></span>

<span data-ttu-id="15f96-162">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="15f96-162">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="15f96-164">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="15f96-164">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="15f96-165">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="15f96-165">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/mercell-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="15f96-167">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="15f96-167">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/mercell-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="15f96-169">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="15f96-169">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/mercell-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="15f96-171">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="15f96-171">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/mercell-tutorial/create_aaduser_04.png)

    <span data-ttu-id="15f96-173">a.</span><span class="sxs-lookup"><span data-stu-id="15f96-173">a.</span></span> <span data-ttu-id="15f96-174">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="15f96-174">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="15f96-175">b.</span><span class="sxs-lookup"><span data-stu-id="15f96-175">b.</span></span> <span data-ttu-id="15f96-176">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="15f96-176">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="15f96-177">c.</span><span class="sxs-lookup"><span data-stu-id="15f96-177">c.</span></span> <span data-ttu-id="15f96-178">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="15f96-178">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="15f96-179">d.</span><span class="sxs-lookup"><span data-stu-id="15f96-179">d.</span></span> <span data-ttu-id="15f96-180">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="15f96-180">Click **Create**.</span></span>
 
### <a name="create-a-mercell-test-user"></a><span data-ttu-id="15f96-181">Create a Mercell test user</span><span class="sxs-lookup"><span data-stu-id="15f96-181">Create a Mercell test user</span></span>

<span data-ttu-id="15f96-182">The objective of this section is to create a user called Britta Simon in Mercell.</span><span class="sxs-lookup"><span data-stu-id="15f96-182">The objective of this section is to create a user called Britta Simon in Mercell.</span></span> <span data-ttu-id="15f96-183">Mercell supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="15f96-183">Mercell supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="15f96-184">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="15f96-184">There is no action item for you in this section.</span></span> <span data-ttu-id="15f96-185">A new user is created during an attempt to access Mercell if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="15f96-185">A new user is created during an attempt to access Mercell if it doesn't exist yet.</span></span>
>[!Note]
><span data-ttu-id="15f96-186">If you need to create a user manually, contact [Mercell support team](mailto:webmaster@mercell.com).</span><span class="sxs-lookup"><span data-stu-id="15f96-186">If you need to create a user manually, contact [Mercell support team](mailto:webmaster@mercell.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="15f96-187">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="15f96-187">Assign the Azure AD test user</span></span>

<span data-ttu-id="15f96-188">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mercell.</span><span class="sxs-lookup"><span data-stu-id="15f96-188">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mercell.</span></span>

![Assign the user role][200] 

<span data-ttu-id="15f96-190">**To assign Britta Simon to Mercell, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="15f96-190">**To assign Britta Simon to Mercell, perform the following steps:**</span></span>

1. <span data-ttu-id="15f96-191">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="15f96-191">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="15f96-193">In the applications list, select **Mercell**.</span><span class="sxs-lookup"><span data-stu-id="15f96-193">In the applications list, select **Mercell**.</span></span>

    ![The Mercell link in the Applications list](./media/mercell-tutorial/tutorial_mercell_app.png)  

3. <span data-ttu-id="15f96-195">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="15f96-195">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="15f96-197">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="15f96-197">Click **Add** button.</span></span> <span data-ttu-id="15f96-198">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="15f96-198">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="15f96-200">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="15f96-200">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="15f96-201">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="15f96-201">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="15f96-202">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="15f96-202">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="15f96-203">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="15f96-203">Test single sign-on</span></span>

<span data-ttu-id="15f96-204">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="15f96-204">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="15f96-205">When you click the Mercell tile in the Access Panel, you should get automatically signed-on to your Mercell application.</span><span class="sxs-lookup"><span data-stu-id="15f96-205">When you click the Mercell tile in the Access Panel, you should get automatically signed-on to your Mercell application.</span></span>
<span data-ttu-id="15f96-206">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="15f96-206">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="15f96-207">Additional resources</span><span class="sxs-lookup"><span data-stu-id="15f96-207">Additional resources</span></span>

* [<span data-ttu-id="15f96-208">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="15f96-208">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="15f96-209">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="15f96-209">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/mercell-tutorial/tutorial_general_01.png
[2]: ./media/mercell-tutorial/tutorial_general_02.png
[3]: ./media/mercell-tutorial/tutorial_general_03.png
[4]: ./media/mercell-tutorial/tutorial_general_04.png

[100]: ./media/mercell-tutorial/tutorial_general_100.png

[200]: ./media/mercell-tutorial/tutorial_general_200.png
[201]: ./media/mercell-tutorial/tutorial_general_201.png
[202]: ./media/mercell-tutorial/tutorial_general_202.png
[203]: ./media/mercell-tutorial/tutorial_general_203.png

