---
title: 'Tutorial: Azure Active Directory integration with Skytap | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Skytap.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6cb7ab2-da1a-4015-8e6f-c0c47bb6210f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2018
ms.author: jeedes
ms.openlocfilehash: 754697682470ac3c1f982e6cb1fc5f6043f3b92c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855985"
---
# <a name="tutorial-azure-active-directory-integration-with-skytap"></a><span data-ttu-id="6cc41-103">Tutorial: Azure Active Directory integration with Skytap</span><span class="sxs-lookup"><span data-stu-id="6cc41-103">Tutorial: Azure Active Directory integration with Skytap</span></span>

<span data-ttu-id="6cc41-104">In this tutorial, you learn how to integrate Skytap with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6cc41-104">In this tutorial, you learn how to integrate Skytap with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6cc41-105">Integrating Skytap with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="6cc41-105">Integrating Skytap with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6cc41-106">You can control in Azure AD who has access to Skytap.</span><span class="sxs-lookup"><span data-stu-id="6cc41-106">You can control in Azure AD who has access to Skytap.</span></span>
- <span data-ttu-id="6cc41-107">You can enable your users to automatically get signed-on to Skytap (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="6cc41-107">You can enable your users to automatically get signed-on to Skytap (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6cc41-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6cc41-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="6cc41-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="6cc41-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6cc41-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6cc41-110">Prerequisites</span></span>

<span data-ttu-id="6cc41-111">To configure Azure AD integration with Skytap, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="6cc41-111">To configure Azure AD integration with Skytap, you need the following items:</span></span>

- <span data-ttu-id="6cc41-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="6cc41-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6cc41-113">A Skytap single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="6cc41-113">A Skytap single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6cc41-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="6cc41-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6cc41-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="6cc41-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6cc41-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="6cc41-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6cc41-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6cc41-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6cc41-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="6cc41-118">Scenario description</span></span>
<span data-ttu-id="6cc41-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="6cc41-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6cc41-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="6cc41-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6cc41-121">Adding Skytap from the gallery</span><span class="sxs-lookup"><span data-stu-id="6cc41-121">Adding Skytap from the gallery</span></span>
1. <span data-ttu-id="6cc41-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6cc41-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skytap-from-the-gallery"></a><span data-ttu-id="6cc41-123">Adding Skytap from the gallery</span><span class="sxs-lookup"><span data-stu-id="6cc41-123">Adding Skytap from the gallery</span></span>
<span data-ttu-id="6cc41-124">To configure the integration of Skytap into Azure AD, you need to add Skytap from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="6cc41-124">To configure the integration of Skytap into Azure AD, you need to add Skytap from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6cc41-125">**To add Skytap from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6cc41-125">**To add Skytap from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6cc41-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="6cc41-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="6cc41-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="6cc41-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6cc41-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6cc41-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="6cc41-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="6cc41-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="6cc41-133">In the search box, type **Skytap**, select **Skytap** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="6cc41-133">In the search box, type **Skytap**, select **Skytap** from result panel then click **Add** button to add the application.</span></span>

    ![Skytap in the results list](./media/skytap-tutorial/tutorial_skytap_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6cc41-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6cc41-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6cc41-136">In this section, you configure and test Azure AD single sign-on with Skytap based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6cc41-136">In this section, you configure and test Azure AD single sign-on with Skytap based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6cc41-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Skytap is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6cc41-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Skytap is to a user in Azure AD.</span></span> <span data-ttu-id="6cc41-138">In other words, a link relationship between an Azure AD user and the related user in Skytap needs to be established.</span><span class="sxs-lookup"><span data-stu-id="6cc41-138">In other words, a link relationship between an Azure AD user and the related user in Skytap needs to be established.</span></span>

<span data-ttu-id="6cc41-139">To configure and test Azure AD single sign-on with Skytap, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="6cc41-139">To configure and test Azure AD single sign-on with Skytap, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6cc41-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="6cc41-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="6cc41-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6cc41-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="6cc41-142">**[Create a Skytap test user](#create-a-skytap-test-user)** - to have a counterpart of Britta Simon in Skytap that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="6cc41-142">**[Create a Skytap test user](#create-a-skytap-test-user)** - to have a counterpart of Britta Simon in Skytap that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="6cc41-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6cc41-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="6cc41-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="6cc41-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6cc41-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6cc41-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6cc41-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skytap application.</span><span class="sxs-lookup"><span data-stu-id="6cc41-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Skytap application.</span></span>

<span data-ttu-id="6cc41-147">**To configure Azure AD single sign-on with Skytap, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6cc41-147">**To configure Azure AD single sign-on with Skytap, perform the following steps:**</span></span>

1. <span data-ttu-id="6cc41-148">In the Azure portal, on the **Skytap** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6cc41-148">In the Azure portal, on the **Skytap** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="6cc41-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6cc41-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/skytap-tutorial/tutorial_skytap_samlbase.png)

1. <span data-ttu-id="6cc41-152">On the **Skytap Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="6cc41-152">On the **Skytap Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Skytap Domain and URLs single sign-on information](./media/skytap-tutorial/tutorial_skytap_url.png)

    <span data-ttu-id="6cc41-154">a.</span><span class="sxs-lookup"><span data-stu-id="6cc41-154">a.</span></span> <span data-ttu-id="6cc41-155">In the **Identifier** textbox, type a URL using the following pattern: `http://pingone.com/<custom EntityID>`</span><span class="sxs-lookup"><span data-stu-id="6cc41-155">In the **Identifier** textbox, type a URL using the following pattern: `http://pingone.com/<custom EntityID>`</span></span>

    <span data-ttu-id="6cc41-156">b.</span><span class="sxs-lookup"><span data-stu-id="6cc41-156">b.</span></span> <span data-ttu-id="6cc41-157">In the **Reply URL** textbox, type a URL: `https://sso.connect.pingidentity.com/sso/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="6cc41-157">In the **Reply URL** textbox, type a URL: `https://sso.connect.pingidentity.com/sso/sp/ACS.saml2`</span></span>

1. <span data-ttu-id="6cc41-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="6cc41-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Skytap Domain and URLs single sign-on information](./media/skytap-tutorial/tutorial_skytap_url1.png)

    <span data-ttu-id="6cc41-160">c.</span><span class="sxs-lookup"><span data-stu-id="6cc41-160">c.</span></span> <span data-ttu-id="6cc41-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.connect.pingidentity.com/sso/sp/initsso?saasid=<saasid>&idpid=<idpid>`</span><span class="sxs-lookup"><span data-stu-id="6cc41-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.connect.pingidentity.com/sso/sp/initsso?saasid=<saasid>&idpid=<idpid>`</span></span>
     
    <span data-ttu-id="6cc41-162">d.</span><span class="sxs-lookup"><span data-stu-id="6cc41-162">d.</span></span> <span data-ttu-id="6cc41-163">In the **Relay State** textbox, type a URL using the following pattern: `https://pingone.com/1.0/<custom ID>`</span><span class="sxs-lookup"><span data-stu-id="6cc41-163">In the **Relay State** textbox, type a URL using the following pattern: `https://pingone.com/1.0/<custom ID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6cc41-164">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="6cc41-164">These values are not real.</span></span> <span data-ttu-id="6cc41-165">Update these values with the actual Identifier, Sign-On URL and Relay State.</span><span class="sxs-lookup"><span data-stu-id="6cc41-165">Update these values with the actual Identifier, Sign-On URL and Relay State.</span></span> <span data-ttu-id="6cc41-166">Contact [Skytap Client support team](mailto:support@skytap.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="6cc41-166">Contact [Skytap Client support team](mailto:support@skytap.com) to get these values.</span></span> 

1. <span data-ttu-id="6cc41-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="6cc41-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/skytap-tutorial/tutorial_skytap_certificate.png) 

1. <span data-ttu-id="6cc41-169">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="6cc41-169">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/skytap-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="6cc41-171">To configure single sign-on on **Skytap** side, you need to send the downloaded **Metadata XML** to [Skytap support team](mailto:support@skytap.com).</span><span class="sxs-lookup"><span data-stu-id="6cc41-171">To configure single sign-on on **Skytap** side, you need to send the downloaded **Metadata XML** to [Skytap support team](mailto:support@skytap.com).</span></span> <span data-ttu-id="6cc41-172">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="6cc41-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6cc41-173">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6cc41-173">Create an Azure AD test user</span></span>

<span data-ttu-id="6cc41-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6cc41-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="6cc41-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6cc41-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6cc41-177">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="6cc41-177">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/skytap-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="6cc41-179">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="6cc41-179">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/skytap-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="6cc41-181">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="6cc41-181">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/skytap-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="6cc41-183">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6cc41-183">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/skytap-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6cc41-185">a.</span><span class="sxs-lookup"><span data-stu-id="6cc41-185">a.</span></span> <span data-ttu-id="6cc41-186">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6cc41-186">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6cc41-187">b.</span><span class="sxs-lookup"><span data-stu-id="6cc41-187">b.</span></span> <span data-ttu-id="6cc41-188">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6cc41-188">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="6cc41-189">c.</span><span class="sxs-lookup"><span data-stu-id="6cc41-189">c.</span></span> <span data-ttu-id="6cc41-190">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="6cc41-190">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="6cc41-191">d.</span><span class="sxs-lookup"><span data-stu-id="6cc41-191">d.</span></span> <span data-ttu-id="6cc41-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6cc41-192">Click **Create**.</span></span>
 
### <a name="create-a-skytap-test-user"></a><span data-ttu-id="6cc41-193">Create a Skytap test user</span><span class="sxs-lookup"><span data-stu-id="6cc41-193">Create a Skytap test user</span></span>

<span data-ttu-id="6cc41-194">In this section, you create a user called Britta Simon in Skytap.</span><span class="sxs-lookup"><span data-stu-id="6cc41-194">In this section, you create a user called Britta Simon in Skytap.</span></span> <span data-ttu-id="6cc41-195">Work with [Skytap support team](mailto:support@skytap.com) to add the users in the Skytap platform.</span><span class="sxs-lookup"><span data-stu-id="6cc41-195">Work with [Skytap support team](mailto:support@skytap.com) to add the users in the Skytap platform.</span></span> <span data-ttu-id="6cc41-196">Users must be created and activated before you use single sign-on</span><span class="sxs-lookup"><span data-stu-id="6cc41-196">Users must be created and activated before you use single sign-on</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6cc41-197">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6cc41-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="6cc41-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skytap.</span><span class="sxs-lookup"><span data-stu-id="6cc41-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Skytap.</span></span>

![Assign the user role][200] 

<span data-ttu-id="6cc41-200">**To assign Britta Simon to Skytap, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6cc41-200">**To assign Britta Simon to Skytap, perform the following steps:**</span></span>

1. <span data-ttu-id="6cc41-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6cc41-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="6cc41-203">In the applications list, select **Skytap**.</span><span class="sxs-lookup"><span data-stu-id="6cc41-203">In the applications list, select **Skytap**.</span></span>

    ![The Skytap link in the Applications list](./media/skytap-tutorial/tutorial_skytap_app.png)  

1. <span data-ttu-id="6cc41-205">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="6cc41-205">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="6cc41-207">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="6cc41-207">Click **Add** button.</span></span> <span data-ttu-id="6cc41-208">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6cc41-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="6cc41-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="6cc41-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="6cc41-211">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="6cc41-211">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="6cc41-212">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6cc41-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6cc41-213">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="6cc41-213">Test single sign-on</span></span>

<span data-ttu-id="6cc41-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="6cc41-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6cc41-215">When you click the Skytap tile in the Access Panel, you should get automatically signed-on to your Skytap application.</span><span class="sxs-lookup"><span data-stu-id="6cc41-215">When you click the Skytap tile in the Access Panel, you should get automatically signed-on to your Skytap application.</span></span>
<span data-ttu-id="6cc41-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6cc41-216">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6cc41-217">Additional resources</span><span class="sxs-lookup"><span data-stu-id="6cc41-217">Additional resources</span></span>

* [<span data-ttu-id="6cc41-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6cc41-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="6cc41-219">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6cc41-219">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/skytap-tutorial/tutorial_general_01.png
[2]: ./media/skytap-tutorial/tutorial_general_02.png
[3]: ./media/skytap-tutorial/tutorial_general_03.png
[4]: ./media/skytap-tutorial/tutorial_general_04.png

[100]: ./media/skytap-tutorial/tutorial_general_100.png

[200]: ./media/skytap-tutorial/tutorial_general_200.png
[201]: ./media/skytap-tutorial/tutorial_general_201.png
[202]: ./media/skytap-tutorial/tutorial_general_202.png
[203]: ./media/skytap-tutorial/tutorial_general_203.png

