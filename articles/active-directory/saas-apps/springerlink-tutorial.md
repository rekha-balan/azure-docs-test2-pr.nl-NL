---
title: 'Tutorial: Azure Active Directory integration with Springer Link | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Springer Link.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 58cdf029-bdc0-43c4-a469-b921c2a669bd
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: jeedes
ms.openlocfilehash: 8138c7605b0024dfe4569e33843cb1e9d169271f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864790"
---
# <a name="tutorial-azure-active-directory-integration-with-springer-link"></a><span data-ttu-id="332d5-103">Tutorial: Azure Active Directory integration with Springer Link</span><span class="sxs-lookup"><span data-stu-id="332d5-103">Tutorial: Azure Active Directory integration with Springer Link</span></span>

<span data-ttu-id="332d5-104">In this tutorial, you learn how to integrate Springer Link with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="332d5-104">In this tutorial, you learn how to integrate Springer Link with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="332d5-105">Integrating Springer Link with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="332d5-105">Integrating Springer Link with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="332d5-106">You can control in Azure AD who has access to Springer Link.</span><span class="sxs-lookup"><span data-stu-id="332d5-106">You can control in Azure AD who has access to Springer Link.</span></span>
- <span data-ttu-id="332d5-107">You can enable your users to automatically get signed-on to Springer Link (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="332d5-107">You can enable your users to automatically get signed-on to Springer Link (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="332d5-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="332d5-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="332d5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="332d5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="332d5-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="332d5-110">Prerequisites</span></span>

<span data-ttu-id="332d5-111">To configure Azure AD integration with Springer Link, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="332d5-111">To configure Azure AD integration with Springer Link, you need the following items:</span></span>

- <span data-ttu-id="332d5-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="332d5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="332d5-113">A Springer Link single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="332d5-113">A Springer Link single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="332d5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="332d5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="332d5-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="332d5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="332d5-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="332d5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="332d5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="332d5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="332d5-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="332d5-118">Scenario description</span></span>
<span data-ttu-id="332d5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="332d5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="332d5-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="332d5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="332d5-121">Adding Springer Link from the gallery</span><span class="sxs-lookup"><span data-stu-id="332d5-121">Adding Springer Link from the gallery</span></span>
1. <span data-ttu-id="332d5-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="332d5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springer-link-from-the-gallery"></a><span data-ttu-id="332d5-123">Adding Springer Link from the gallery</span><span class="sxs-lookup"><span data-stu-id="332d5-123">Adding Springer Link from the gallery</span></span>
<span data-ttu-id="332d5-124">To configure the integration of Springer Link into Azure AD, you need to add Springer Link from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="332d5-124">To configure the integration of Springer Link into Azure AD, you need to add Springer Link from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="332d5-125">**To add Springer Link from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="332d5-125">**To add Springer Link from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="332d5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="332d5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="332d5-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="332d5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="332d5-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="332d5-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="332d5-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="332d5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="332d5-133">In the search box, type **Springer Link**, select **Springer Link** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="332d5-133">In the search box, type **Springer Link**, select **Springer Link** from result panel then click **Add** button to add the application.</span></span>

    ![Springer Link in the results list](./media/springerlink-tutorial/tutorial_springerlink_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="332d5-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="332d5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="332d5-136">In this section, you configure and test Azure AD single sign-on with Springer Link based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="332d5-136">In this section, you configure and test Azure AD single sign-on with Springer Link based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="332d5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Springer Link is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="332d5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Springer Link is to a user in Azure AD.</span></span> <span data-ttu-id="332d5-138">In other words, a link relationship between an Azure AD user and the related user in Springer Link needs to be established.</span><span class="sxs-lookup"><span data-stu-id="332d5-138">In other words, a link relationship between an Azure AD user and the related user in Springer Link needs to be established.</span></span>

<span data-ttu-id="332d5-139">In Springer Link, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="332d5-139">In Springer Link, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="332d5-140">To configure and test Azure AD single sign-on with Springer Link, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="332d5-140">To configure and test Azure AD single sign-on with Springer Link, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="332d5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="332d5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="332d5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="332d5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="332d5-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="332d5-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="332d5-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="332d5-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="332d5-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="332d5-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="332d5-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Springer Link application.</span><span class="sxs-lookup"><span data-stu-id="332d5-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Springer Link application.</span></span>

<span data-ttu-id="332d5-147">**To configure Azure AD single sign-on with Springer Link, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="332d5-147">**To configure Azure AD single sign-on with Springer Link, perform the following steps:**</span></span>

1. <span data-ttu-id="332d5-148">In the Azure portal, on the **Springer Link** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="332d5-148">In the Azure portal, on the **Springer Link** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="332d5-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="332d5-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/springerlink-tutorial/tutorial_springerlink_samlbase.png)

1. <span data-ttu-id="332d5-152">On the **Springer Link Domain and URLs** section,  If you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="332d5-152">On the **Springer Link Domain and URLs** section,  If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Springer Link Domain and URLs single sign-on information](./media/springerlink-tutorial/tutorial_springerlink_url1.png)

    <span data-ttu-id="332d5-154">a.</span><span class="sxs-lookup"><span data-stu-id="332d5-154">a.</span></span> <span data-ttu-id="332d5-155">In the **Identifier** textbox, type the URL: `https://fsso.springer.com`</span><span class="sxs-lookup"><span data-stu-id="332d5-155">In the **Identifier** textbox, type the URL: `https://fsso.springer.com`</span></span>

    <span data-ttu-id="332d5-156">b.</span><span class="sxs-lookup"><span data-stu-id="332d5-156">b.</span></span> <span data-ttu-id="332d5-157">In the **Reply URL** textbox, type the URL: `https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="332d5-157">In the **Reply URL** textbox, type the URL: `https://fsso-qa1.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>    

1. <span data-ttu-id="332d5-158">Check **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="332d5-158">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="332d5-159">If you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="332d5-159">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Springer Link Domain and URLs single sign-on information](./media/springerlink-tutorial/tutorial_springerlink_url.png)

    <span data-ttu-id="332d5-161">In the **Sign-on URL** textbox, type the URL : `https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span><span class="sxs-lookup"><span data-stu-id="332d5-161">In the **Sign-on URL** textbox, type the URL : `https://fsso.springer.com/federation/Consumer/metaAlias/SpringerServiceProvider`</span></span>

1. <span data-ttu-id="332d5-162">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="332d5-162">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span> 

    ![The Certificate download link](./media/springerlink-tutorial/tutorial_springerlink_certificate.png)    

1. <span data-ttu-id="332d5-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="332d5-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/springerlink-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="332d5-166">To configure single sign-on on **Springer Link** side, you need to send the **App Federation Metadata Url** to [Springer Link support team](mailto:identity@springernature.com).</span><span class="sxs-lookup"><span data-stu-id="332d5-166">To configure single sign-on on **Springer Link** side, you need to send the **App Federation Metadata Url** to [Springer Link support team](mailto:identity@springernature.com).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="332d5-167">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="332d5-167">Create an Azure AD test user</span></span>

<span data-ttu-id="332d5-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="332d5-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="332d5-170">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="332d5-170">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="332d5-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="332d5-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/springerlink-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="332d5-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="332d5-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/springerlink-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="332d5-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="332d5-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/springerlink-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="332d5-177">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="332d5-177">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/springerlink-tutorial/create_aaduser_04.png)

    <span data-ttu-id="332d5-179">a.</span><span class="sxs-lookup"><span data-stu-id="332d5-179">a.</span></span> <span data-ttu-id="332d5-180">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="332d5-180">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="332d5-181">b.</span><span class="sxs-lookup"><span data-stu-id="332d5-181">b.</span></span> <span data-ttu-id="332d5-182">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="332d5-182">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="332d5-183">c.</span><span class="sxs-lookup"><span data-stu-id="332d5-183">c.</span></span> <span data-ttu-id="332d5-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="332d5-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="332d5-185">d.</span><span class="sxs-lookup"><span data-stu-id="332d5-185">d.</span></span> <span data-ttu-id="332d5-186">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="332d5-186">Click **Create**.</span></span>
 
### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="332d5-187">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="332d5-187">Assign the Azure AD test user</span></span>

<span data-ttu-id="332d5-188">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Springer Link.</span><span class="sxs-lookup"><span data-stu-id="332d5-188">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Springer Link.</span></span>

![Assign the user role][200] 

<span data-ttu-id="332d5-190">**To assign Britta Simon to Springer Link, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="332d5-190">**To assign Britta Simon to Springer Link, perform the following steps:**</span></span>

1. <span data-ttu-id="332d5-191">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="332d5-191">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="332d5-193">In the applications list, select **Springer Link**.</span><span class="sxs-lookup"><span data-stu-id="332d5-193">In the applications list, select **Springer Link**.</span></span>

    ![The Springer Link link in the Applications list](./media/springerlink-tutorial/tutorial_springerlink_app.png)  

1. <span data-ttu-id="332d5-195">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="332d5-195">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="332d5-197">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="332d5-197">Click **Add** button.</span></span> <span data-ttu-id="332d5-198">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="332d5-198">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="332d5-200">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="332d5-200">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="332d5-201">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="332d5-201">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="332d5-202">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="332d5-202">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="332d5-203">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="332d5-203">Test single sign-on</span></span>

<span data-ttu-id="332d5-204">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="332d5-204">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="332d5-205">When you click the Springer Link tile in the Access Panel, you should get automatically signed-on to your Springer Link application.</span><span class="sxs-lookup"><span data-stu-id="332d5-205">When you click the Springer Link tile in the Access Panel, you should get automatically signed-on to your Springer Link application.</span></span>
<span data-ttu-id="332d5-206">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="332d5-206">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="332d5-207">Additional resources</span><span class="sxs-lookup"><span data-stu-id="332d5-207">Additional resources</span></span>

* [<span data-ttu-id="332d5-208">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="332d5-208">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="332d5-209">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="332d5-209">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/springerlink-tutorial/tutorial_general_01.png
[2]: ./media/springerlink-tutorial/tutorial_general_02.png
[3]: ./media/springerlink-tutorial/tutorial_general_03.png
[4]: ./media/springerlink-tutorial/tutorial_general_04.png

[100]: ./media/springerlink-tutorial/tutorial_general_100.png

[200]: ./media/springerlink-tutorial/tutorial_general_200.png
[201]: ./media/springerlink-tutorial/tutorial_general_201.png
[202]: ./media/springerlink-tutorial/tutorial_general_202.png
[203]: ./media/springerlink-tutorial/tutorial_general_203.png

