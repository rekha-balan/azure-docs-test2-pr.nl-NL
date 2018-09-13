---
title: 'Tutorial: Azure Active Directory integration with PlanGrid | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and PlanGrid.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0ba72432-9b49-4358-b756-14c982422be8
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2018
ms.author: jeedes
ms.openlocfilehash: b2225a48e78e8c609223510a32d3ed5c735ed3b6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869793"
---
# <a name="tutorial-azure-active-directory-integration-with-plangrid"></a><span data-ttu-id="c562d-103">Tutorial: Azure Active Directory integration with PlanGrid</span><span class="sxs-lookup"><span data-stu-id="c562d-103">Tutorial: Azure Active Directory integration with PlanGrid</span></span>

<span data-ttu-id="c562d-104">In this tutorial, you learn how to integrate PlanGrid with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c562d-104">In this tutorial, you learn how to integrate PlanGrid with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c562d-105">Integrating PlanGrid with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="c562d-105">Integrating PlanGrid with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c562d-106">You can control in Azure AD who has access to PlanGrid.</span><span class="sxs-lookup"><span data-stu-id="c562d-106">You can control in Azure AD who has access to PlanGrid.</span></span>
- <span data-ttu-id="c562d-107">You can enable your users to automatically get signed-on to PlanGrid (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="c562d-107">You can enable your users to automatically get signed-on to PlanGrid (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="c562d-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c562d-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="c562d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="c562d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c562d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c562d-110">Prerequisites</span></span>

<span data-ttu-id="c562d-111">To configure Azure AD integration with PlanGrid, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="c562d-111">To configure Azure AD integration with PlanGrid, you need the following items:</span></span>

- <span data-ttu-id="c562d-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="c562d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c562d-113">A PlanGrid single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="c562d-113">A PlanGrid single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c562d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="c562d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c562d-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="c562d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c562d-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="c562d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c562d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c562d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c562d-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="c562d-118">Scenario description</span></span>
<span data-ttu-id="c562d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="c562d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c562d-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="c562d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c562d-121">Adding PlanGrid from the gallery</span><span class="sxs-lookup"><span data-stu-id="c562d-121">Adding PlanGrid from the gallery</span></span>
2. <span data-ttu-id="c562d-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c562d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-plangrid-from-the-gallery"></a><span data-ttu-id="c562d-123">Adding PlanGrid from the gallery</span><span class="sxs-lookup"><span data-stu-id="c562d-123">Adding PlanGrid from the gallery</span></span>
<span data-ttu-id="c562d-124">To configure the integration of PlanGrid into Azure AD, you need to add PlanGrid from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="c562d-124">To configure the integration of PlanGrid into Azure AD, you need to add PlanGrid from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c562d-125">**To add PlanGrid from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c562d-125">**To add PlanGrid from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c562d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="c562d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="c562d-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="c562d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c562d-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c562d-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="c562d-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="c562d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="c562d-133">In the search box, type **PlanGrid**, select **PlanGrid** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="c562d-133">In the search box, type **PlanGrid**, select **PlanGrid** from result panel then click **Add** button to add the application.</span></span>

    ![PlanGrid in the results list](./media/plangrid-tutorial/tutorial_plangrid_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c562d-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c562d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="c562d-136">In this section, you configure and test Azure AD single sign-on with PlanGrid based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c562d-136">In this section, you configure and test Azure AD single sign-on with PlanGrid based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c562d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in PlanGrid is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c562d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in PlanGrid is to a user in Azure AD.</span></span> <span data-ttu-id="c562d-138">In other words, a link relationship between an Azure AD user and the related user in PlanGrid needs to be established.</span><span class="sxs-lookup"><span data-stu-id="c562d-138">In other words, a link relationship between an Azure AD user and the related user in PlanGrid needs to be established.</span></span>

<span data-ttu-id="c562d-139">To configure and test Azure AD single sign-on with PlanGrid, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c562d-139">To configure and test Azure AD single sign-on with PlanGrid, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c562d-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="c562d-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c562d-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c562d-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c562d-142">**[Create a PlanGrid test user](#create-a-plangrid-test-user)** - to have a counterpart of Britta Simon in PlanGrid that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="c562d-142">**[Create a PlanGrid test user](#create-a-plangrid-test-user)** - to have a counterpart of Britta Simon in PlanGrid that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c562d-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c562d-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c562d-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="c562d-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c562d-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c562d-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c562d-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PlanGrid application.</span><span class="sxs-lookup"><span data-stu-id="c562d-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PlanGrid application.</span></span>

<span data-ttu-id="c562d-147">**To configure Azure AD single sign-on with PlanGrid, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c562d-147">**To configure Azure AD single sign-on with PlanGrid, perform the following steps:**</span></span>

1. <span data-ttu-id="c562d-148">In the Azure portal, on the **PlanGrid** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c562d-148">In the Azure portal, on the **PlanGrid** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="c562d-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c562d-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/plangrid-tutorial/tutorial_plangrid_samlbase.png)

3. <span data-ttu-id="c562d-152">On the **PlanGrid Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="c562d-152">On the **PlanGrid Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![PlanGrid Domain and URLs single sign-on information](./media/plangrid-tutorial/tutorial_plangrid_url1.png)

    <span data-ttu-id="c562d-154">In the **Identifier (Entity ID)** textbox, type the URL: `https://io.plangrid.com/sessions/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="c562d-154">In the **Identifier (Entity ID)** textbox, type the URL: `https://io.plangrid.com/sessions/saml/metadata`</span></span>

4. <span data-ttu-id="c562d-155">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="c562d-155">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![PlanGrid Domain and URLs single sign-on information](./media/plangrid-tutorial/tutorial_plangrid_url2.png)

    <span data-ttu-id="c562d-157">In the **Sign-on URL** textbox, type the URL: `https://app.plangrid.com/login`</span><span class="sxs-lookup"><span data-stu-id="c562d-157">In the **Sign-on URL** textbox, type the URL: `https://app.plangrid.com/login`</span></span>

5. <span data-ttu-id="c562d-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="c562d-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/plangrid-tutorial/tutorial_plangrid_certificate.png) 

6. <span data-ttu-id="c562d-160">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="c562d-160">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/plangrid-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="c562d-162">To configure single sign-on on **PlanGrid** side, you need to send the downloaded **Metadata XML** to [PlanGrid support team](mailto:help@plangrid.com).</span><span class="sxs-lookup"><span data-stu-id="c562d-162">To configure single sign-on on **PlanGrid** side, you need to send the downloaded **Metadata XML** to [PlanGrid support team](mailto:help@plangrid.com).</span></span> <span data-ttu-id="c562d-163">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="c562d-163">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c562d-164">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c562d-164">Create an Azure AD test user</span></span>

<span data-ttu-id="c562d-165">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c562d-165">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="c562d-167">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c562d-167">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c562d-168">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="c562d-168">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/plangrid-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="c562d-170">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="c562d-170">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/plangrid-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="c562d-172">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="c562d-172">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/plangrid-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="c562d-174">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c562d-174">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/plangrid-tutorial/create_aaduser_04.png)

    <span data-ttu-id="c562d-176">a.</span><span class="sxs-lookup"><span data-stu-id="c562d-176">a.</span></span> <span data-ttu-id="c562d-177">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c562d-177">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c562d-178">b.</span><span class="sxs-lookup"><span data-stu-id="c562d-178">b.</span></span> <span data-ttu-id="c562d-179">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c562d-179">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="c562d-180">c.</span><span class="sxs-lookup"><span data-stu-id="c562d-180">c.</span></span> <span data-ttu-id="c562d-181">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="c562d-181">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="c562d-182">d.</span><span class="sxs-lookup"><span data-stu-id="c562d-182">d.</span></span> <span data-ttu-id="c562d-183">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c562d-183">Click **Create**.</span></span>
 
### <a name="create-a-plangrid-test-user"></a><span data-ttu-id="c562d-184">Create a PlanGrid test user</span><span class="sxs-lookup"><span data-stu-id="c562d-184">Create a PlanGrid test user</span></span>

<span data-ttu-id="c562d-185">In this section, you create a user called Britta Simon in PlanGrid.</span><span class="sxs-lookup"><span data-stu-id="c562d-185">In this section, you create a user called Britta Simon in PlanGrid.</span></span> <span data-ttu-id="c562d-186">Work with [PlanGrid support team](mailto:help@plangrid.com) to add the users in the PlanGrid platform.</span><span class="sxs-lookup"><span data-stu-id="c562d-186">Work with [PlanGrid support team](mailto:help@plangrid.com) to add the users in the PlanGrid platform.</span></span> <span data-ttu-id="c562d-187">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c562d-187">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c562d-188">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c562d-188">Assign the Azure AD test user</span></span>

<span data-ttu-id="c562d-189">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PlanGrid.</span><span class="sxs-lookup"><span data-stu-id="c562d-189">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PlanGrid.</span></span>

![Assign the user role][200] 

<span data-ttu-id="c562d-191">**To assign Britta Simon to PlanGrid, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c562d-191">**To assign Britta Simon to PlanGrid, perform the following steps:**</span></span>

1. <span data-ttu-id="c562d-192">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="c562d-192">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="c562d-194">In the applications list, select **PlanGrid**.</span><span class="sxs-lookup"><span data-stu-id="c562d-194">In the applications list, select **PlanGrid**.</span></span>

    ![The PlanGrid link in the Applications list](./media/plangrid-tutorial/tutorial_plangrid_app.png)  

3. <span data-ttu-id="c562d-196">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="c562d-196">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="c562d-198">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="c562d-198">Click **Add** button.</span></span> <span data-ttu-id="c562d-199">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c562d-199">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="c562d-201">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="c562d-201">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c562d-202">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="c562d-202">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c562d-203">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="c562d-203">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c562d-204">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="c562d-204">Test single sign-on</span></span>

<span data-ttu-id="c562d-205">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c562d-205">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c562d-206">When you click the PlanGrid tile in the Access Panel, you should get automatically signed-on to your PlanGrid application.</span><span class="sxs-lookup"><span data-stu-id="c562d-206">When you click the PlanGrid tile in the Access Panel, you should get automatically signed-on to your PlanGrid application.</span></span>
<span data-ttu-id="c562d-207">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c562d-207">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c562d-208">Additional resources</span><span class="sxs-lookup"><span data-stu-id="c562d-208">Additional resources</span></span>

* [<span data-ttu-id="c562d-209">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c562d-209">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="c562d-210">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c562d-210">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/plangrid-tutorial/tutorial_general_01.png
[2]: ./media/plangrid-tutorial/tutorial_general_02.png
[3]: ./media/plangrid-tutorial/tutorial_general_03.png
[4]: ./media/plangrid-tutorial/tutorial_general_04.png

[100]: ./media/plangrid-tutorial/tutorial_general_100.png

[200]: ./media/plangrid-tutorial/tutorial_general_200.png
[201]: ./media/plangrid-tutorial/tutorial_general_201.png
[202]: ./media/plangrid-tutorial/tutorial_general_202.png
[203]: ./media/plangrid-tutorial/tutorial_general_203.png

