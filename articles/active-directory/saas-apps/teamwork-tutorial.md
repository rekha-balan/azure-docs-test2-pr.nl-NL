---
title: 'Tutorial: Azure Active Directory integration with Teamwork.com | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Teamwork.com.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: bd4413c2-0d7c-41a7-aba4-b7a7a28c9448
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 6be2c9a17e719fb53ab257af77605c49ffea9e86
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864433"
---
# <a name="tutorial-azure-active-directory-integration-with-teamworkcom"></a><span data-ttu-id="8394d-103">Tutorial: Azure Active Directory integration with Teamwork.com</span><span class="sxs-lookup"><span data-stu-id="8394d-103">Tutorial: Azure Active Directory integration with Teamwork.com</span></span>

<span data-ttu-id="8394d-104">In this tutorial, you learn how to integrate Teamwork.com with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8394d-104">In this tutorial, you learn how to integrate Teamwork.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8394d-105">Integrating Teamwork.com with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8394d-105">Integrating Teamwork.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8394d-106">You can control in Azure AD who has access to Teamwork.com.</span><span class="sxs-lookup"><span data-stu-id="8394d-106">You can control in Azure AD who has access to Teamwork.com.</span></span>
- <span data-ttu-id="8394d-107">You can enable your users to automatically get signed-on to Teamwork.com (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="8394d-107">You can enable your users to automatically get signed-on to Teamwork.com (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8394d-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8394d-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="8394d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="8394d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8394d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8394d-110">Prerequisites</span></span>

<span data-ttu-id="8394d-111">To configure Azure AD integration with Teamwork.com, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8394d-111">To configure Azure AD integration with Teamwork.com, you need the following items:</span></span>

- <span data-ttu-id="8394d-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8394d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8394d-113">A Teamwork.com single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8394d-113">A Teamwork.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8394d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8394d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8394d-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8394d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8394d-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="8394d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8394d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8394d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8394d-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="8394d-118">Scenario description</span></span>
<span data-ttu-id="8394d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8394d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8394d-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8394d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8394d-121">Adding Teamwork.com from the gallery</span><span class="sxs-lookup"><span data-stu-id="8394d-121">Adding Teamwork.com from the gallery</span></span>
1. <span data-ttu-id="8394d-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8394d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamworkcom-from-the-gallery"></a><span data-ttu-id="8394d-123">Adding Teamwork.com from the gallery</span><span class="sxs-lookup"><span data-stu-id="8394d-123">Adding Teamwork.com from the gallery</span></span>
<span data-ttu-id="8394d-124">To configure the integration of Teamwork.com into Azure AD, you need to add Teamwork.com from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8394d-124">To configure the integration of Teamwork.com into Azure AD, you need to add Teamwork.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8394d-125">**To add Teamwork.com from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8394d-125">**To add Teamwork.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8394d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8394d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="8394d-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="8394d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8394d-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8394d-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="8394d-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="8394d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="8394d-133">In the search box, type **Teamwork.com**, select **Teamwork.com** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="8394d-133">In the search box, type **Teamwork.com**, select **Teamwork.com** from result panel then click **Add** button to add the application.</span></span>

    ![Teamwork.com in the results list](./media/teamwork-tutorial/tutorial_teamwork_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8394d-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8394d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8394d-136">In this section, you configure and test Azure AD single sign-on with Teamwork.com based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8394d-136">In this section, you configure and test Azure AD single sign-on with Teamwork.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8394d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamwork.com is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8394d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamwork.com is to a user in Azure AD.</span></span> <span data-ttu-id="8394d-138">In other words, a link relationship between an Azure AD user and the related user in Teamwork.com needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8394d-138">In other words, a link relationship between an Azure AD user and the related user in Teamwork.com needs to be established.</span></span>

<span data-ttu-id="8394d-139">In Teamwork.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="8394d-139">In Teamwork.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8394d-140">To configure and test Azure AD single sign-on with Teamwork.com, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8394d-140">To configure and test Azure AD single sign-on with Teamwork.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8394d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8394d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="8394d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8394d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="8394d-143">**[Create a Teamwork.com test user](#create-a-teamworkcom-test-user)** - to have a counterpart of Britta Simon in Teamwork.com that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="8394d-143">**[Create a Teamwork.com test user](#create-a-teamworkcom-test-user)** - to have a counterpart of Britta Simon in Teamwork.com that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="8394d-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8394d-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="8394d-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8394d-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8394d-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8394d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8394d-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Teamwork.com application.</span><span class="sxs-lookup"><span data-stu-id="8394d-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Teamwork.com application.</span></span>

<span data-ttu-id="8394d-148">**To configure Azure AD single sign-on with Teamwork.com, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8394d-148">**To configure Azure AD single sign-on with Teamwork.com, perform the following steps:**</span></span>

1. <span data-ttu-id="8394d-149">In the Azure portal, on the **Teamwork.com** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8394d-149">In the Azure portal, on the **Teamwork.com** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="8394d-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8394d-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/teamwork-tutorial/tutorial_teamwork_samlbase.png)

1. <span data-ttu-id="8394d-153">On the **Teamwork.com Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8394d-153">On the **Teamwork.com Domain and URLs** section, perform the following steps:</span></span>

    ![Teamwork.com Domain and URLs single sign-on information](./media/teamwork-tutorial/tutorial_teamwork_url.png)

    <span data-ttu-id="8394d-155">a.</span><span class="sxs-lookup"><span data-stu-id="8394d-155">a.</span></span> <span data-ttu-id="8394d-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.teamwork.com`</span><span class="sxs-lookup"><span data-stu-id="8394d-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.teamwork.com`</span></span>

    <span data-ttu-id="8394d-157">b.</span><span class="sxs-lookup"><span data-stu-id="8394d-157">b.</span></span> <span data-ttu-id="8394d-158">In the **Identifier** textbox, type the URL:</span><span class="sxs-lookup"><span data-stu-id="8394d-158">In the **Identifier** textbox, type the URL:</span></span>

    |||
    |-|-|
    | `https://teamwork.com/saml`|
    | `https://eu.teamwork.com/saml`|

    > [!NOTE] 
    > <span data-ttu-id="8394d-159">This  Sign-on URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="8394d-159">This  Sign-on URL value is not real.</span></span> <span data-ttu-id="8394d-160">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="8394d-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="8394d-161">Contact [Teamwork.com support team](mailto:support@teamwork.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="8394d-161">Contact [Teamwork.com support team](mailto:support@teamwork.com) to get this value.</span></span> 

1. <span data-ttu-id="8394d-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8394d-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/teamwork-tutorial/tutorial_teamwork_certificate.png) 

1. <span data-ttu-id="8394d-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="8394d-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/teamwork-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="8394d-166">To configure single sign-on on **Teamwork.com** side, you need to send the downloaded **Metadata XML** to [Teamwork.com support team](mailto:support@teamwork.com).</span><span class="sxs-lookup"><span data-stu-id="8394d-166">To configure single sign-on on **Teamwork.com** side, you need to send the downloaded **Metadata XML** to [Teamwork.com support team](mailto:support@teamwork.com).</span></span> <span data-ttu-id="8394d-167">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="8394d-167">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8394d-168">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8394d-168">Create an Azure AD test user</span></span>

<span data-ttu-id="8394d-169">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8394d-169">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="8394d-171">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8394d-171">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8394d-172">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="8394d-172">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/teamwork-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="8394d-174">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="8394d-174">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/teamwork-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="8394d-176">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="8394d-176">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/teamwork-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="8394d-178">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8394d-178">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/teamwork-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8394d-180">a.</span><span class="sxs-lookup"><span data-stu-id="8394d-180">a.</span></span> <span data-ttu-id="8394d-181">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8394d-181">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8394d-182">b.</span><span class="sxs-lookup"><span data-stu-id="8394d-182">b.</span></span> <span data-ttu-id="8394d-183">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8394d-183">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="8394d-184">c.</span><span class="sxs-lookup"><span data-stu-id="8394d-184">c.</span></span> <span data-ttu-id="8394d-185">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="8394d-185">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="8394d-186">d.</span><span class="sxs-lookup"><span data-stu-id="8394d-186">d.</span></span> <span data-ttu-id="8394d-187">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8394d-187">Click **Create**.</span></span>
 
### <a name="create-a-teamworkcom-test-user"></a><span data-ttu-id="8394d-188">Create a Teamwork.com test user</span><span class="sxs-lookup"><span data-stu-id="8394d-188">Create a Teamwork.com test user</span></span>

<span data-ttu-id="8394d-189">In this section, you create a user called Britta Simon in Teamwork.com.</span><span class="sxs-lookup"><span data-stu-id="8394d-189">In this section, you create a user called Britta Simon in Teamwork.com.</span></span> <span data-ttu-id="8394d-190">Work with [Teamwork.com support team](mailto:support@teamwork.com) to add the users in the Teamwork.com platform.</span><span class="sxs-lookup"><span data-stu-id="8394d-190">Work with [Teamwork.com support team](mailto:support@teamwork.com) to add the users in the Teamwork.com platform.</span></span> <span data-ttu-id="8394d-191">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8394d-191">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8394d-192">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8394d-192">Assign the Azure AD test user</span></span>

<span data-ttu-id="8394d-193">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Teamwork.com.</span><span class="sxs-lookup"><span data-stu-id="8394d-193">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Teamwork.com.</span></span>

![Assign the user role][200] 

<span data-ttu-id="8394d-195">**To assign Britta Simon to Teamwork.com, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8394d-195">**To assign Britta Simon to Teamwork.com, perform the following steps:**</span></span>

1. <span data-ttu-id="8394d-196">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8394d-196">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="8394d-198">In the applications list, select **Teamwork.com**.</span><span class="sxs-lookup"><span data-stu-id="8394d-198">In the applications list, select **Teamwork.com**.</span></span>

    ![The Teamwork.com link in the Applications list](./media/teamwork-tutorial/tutorial_teamwork_app.png)  

1. <span data-ttu-id="8394d-200">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="8394d-200">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="8394d-202">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="8394d-202">Click **Add** button.</span></span> <span data-ttu-id="8394d-203">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8394d-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="8394d-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="8394d-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="8394d-206">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="8394d-206">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="8394d-207">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8394d-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8394d-208">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="8394d-208">Test single sign-on</span></span>

<span data-ttu-id="8394d-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8394d-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8394d-210">When you click the Teamwork.com tile in the Access Panel, you should get automatically signed-on to your Teamwork.com application.</span><span class="sxs-lookup"><span data-stu-id="8394d-210">When you click the Teamwork.com tile in the Access Panel, you should get automatically signed-on to your Teamwork.com application.</span></span>
<span data-ttu-id="8394d-211">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8394d-211">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8394d-212">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8394d-212">Additional resources</span></span>

* [<span data-ttu-id="8394d-213">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8394d-213">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="8394d-214">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8394d-214">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/teamwork-tutorial/tutorial_general_01.png
[2]: ./media/teamwork-tutorial/tutorial_general_02.png
[3]: ./media/teamwork-tutorial/tutorial_general_03.png
[4]: ./media/teamwork-tutorial/tutorial_general_04.png

[100]: ./media/teamwork-tutorial/tutorial_general_100.png

[200]: ./media/teamwork-tutorial/tutorial_general_200.png
[201]: ./media/teamwork-tutorial/tutorial_general_201.png
[202]: ./media/teamwork-tutorial/tutorial_general_202.png
[203]: ./media/teamwork-tutorial/tutorial_general_203.png

