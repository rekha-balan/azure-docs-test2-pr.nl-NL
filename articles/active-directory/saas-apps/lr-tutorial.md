---
title: 'Tutorial: Azure Active Directory integration with LoginRadius | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and LoginRadius.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5715579e-598f-4d2e-970a-107b80b97be4
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2018
ms.author: jeedes
ms.openlocfilehash: 4c5ce02efb48b5b49f6e861dac90f4d59e4ded39
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864514"
---
# <a name="tutorial-azure-active-directory-integration-with-loginradius"></a><span data-ttu-id="d7774-103">Tutorial: Azure Active Directory integration with LoginRadius</span><span class="sxs-lookup"><span data-stu-id="d7774-103">Tutorial: Azure Active Directory integration with LoginRadius</span></span>

<span data-ttu-id="d7774-104">In this tutorial, you learn how to integrate LoginRadius with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d7774-104">In this tutorial, you learn how to integrate LoginRadius with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d7774-105">Integrating LoginRadius with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d7774-105">Integrating LoginRadius with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d7774-106">You can control in Azure AD who has access to LoginRadius.</span><span class="sxs-lookup"><span data-stu-id="d7774-106">You can control in Azure AD who has access to LoginRadius.</span></span>
- <span data-ttu-id="d7774-107">You can enable your users to automatically get signed-on to LoginRadius (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="d7774-107">You can enable your users to automatically get signed-on to LoginRadius (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d7774-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d7774-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="d7774-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="d7774-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7774-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d7774-110">Prerequisites</span></span>

<span data-ttu-id="d7774-111">To configure Azure AD integration with LoginRadius, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d7774-111">To configure Azure AD integration with LoginRadius, you need the following items:</span></span>

- <span data-ttu-id="d7774-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d7774-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d7774-113">A LoginRadius single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d7774-113">A LoginRadius single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d7774-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d7774-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d7774-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d7774-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d7774-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="d7774-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d7774-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d7774-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d7774-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="d7774-118">Scenario description</span></span>
<span data-ttu-id="d7774-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d7774-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d7774-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d7774-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d7774-121">Adding LoginRadius from the gallery</span><span class="sxs-lookup"><span data-stu-id="d7774-121">Adding LoginRadius from the gallery</span></span>
1. <span data-ttu-id="d7774-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d7774-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-loginradius-from-the-gallery"></a><span data-ttu-id="d7774-123">Adding LoginRadius from the gallery</span><span class="sxs-lookup"><span data-stu-id="d7774-123">Adding LoginRadius from the gallery</span></span>
<span data-ttu-id="d7774-124">To configure the integration of LoginRadius into Azure AD, you need to add LoginRadius from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d7774-124">To configure the integration of LoginRadius into Azure AD, you need to add LoginRadius from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d7774-125">**To add LoginRadius from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d7774-125">**To add LoginRadius from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d7774-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d7774-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="d7774-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="d7774-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d7774-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d7774-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="d7774-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="d7774-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="d7774-133">In the search box, type **LoginRadius**, select **LoginRadius** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="d7774-133">In the search box, type **LoginRadius**, select **LoginRadius** from result panel then click **Add** button to add the application.</span></span>

    ![LoginRadius in the results list](./media/lr-tutorial/tutorial_LoginRadius_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d7774-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d7774-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d7774-136">In this section, you configure and test Azure AD single sign-on with LoginRadius based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d7774-136">In this section, you configure and test Azure AD single sign-on with LoginRadius based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d7774-137">For single sign-on to work, Azure AD needs to know what the counterpart user in LoginRadius is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d7774-137">For single sign-on to work, Azure AD needs to know what the counterpart user in LoginRadius is to a user in Azure AD.</span></span> <span data-ttu-id="d7774-138">In other words, a link relationship between an Azure AD user and the related user in LoginRadius needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d7774-138">In other words, a link relationship between an Azure AD user and the related user in LoginRadius needs to be established.</span></span>

<span data-ttu-id="d7774-139">To configure and test Azure AD single sign-on with LoginRadius, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d7774-139">To configure and test Azure AD single sign-on with LoginRadius, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d7774-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d7774-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="d7774-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d7774-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="d7774-142">**[Create a LoginRadius test user](#create-a-loginradius-test-user)** - to have a counterpart of Britta Simon in LoginRadius that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="d7774-142">**[Create a LoginRadius test user](#create-a-loginradius-test-user)** - to have a counterpart of Britta Simon in LoginRadius that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="d7774-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d7774-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="d7774-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d7774-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d7774-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d7774-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d7774-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LoginRadius application.</span><span class="sxs-lookup"><span data-stu-id="d7774-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LoginRadius application.</span></span>

<span data-ttu-id="d7774-147">**To configure Azure AD single sign-on with LoginRadius, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d7774-147">**To configure Azure AD single sign-on with LoginRadius, perform the following steps:**</span></span>

1. <span data-ttu-id="d7774-148">In the Azure portal, on the **LoginRadius** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d7774-148">In the Azure portal, on the **LoginRadius** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="d7774-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d7774-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/lr-tutorial/tutorial_LoginRadius_samlbase.png)

1. <span data-ttu-id="d7774-152">On the **LoginRadius Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d7774-152">On the **LoginRadius Domain and URLs** section, perform the following steps:</span></span>

    ![LoginRadius Domain and URLs single sign-on information](./media/lr-tutorial/tutorial_LoginRadius_url.png)

    <span data-ttu-id="d7774-154">a.</span><span class="sxs-lookup"><span data-stu-id="d7774-154">a.</span></span>  <span data-ttu-id="d7774-155">In the **Sign-on URL** textbox, type a URL: `https://secure.loginradius.com/login`</span><span class="sxs-lookup"><span data-stu-id="d7774-155">In the **Sign-on URL** textbox, type a URL: `https://secure.loginradius.com/login`</span></span>

    <span data-ttu-id="d7774-156">b.</span><span class="sxs-lookup"><span data-stu-id="d7774-156">b.</span></span> <span data-ttu-id="d7774-157">In the **Identifier** textbox, type a URL: `https://LoginRadius.hub.loginradius.com/`</span><span class="sxs-lookup"><span data-stu-id="d7774-157">In the **Identifier** textbox, type a URL: `https://LoginRadius.hub.loginradius.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="d7774-158">Open the Sign-on URL page.</span><span class="sxs-lookup"><span data-stu-id="d7774-158">Open the Sign-on URL page.</span></span> <span data-ttu-id="d7774-159">Click on **Single Sign-On** tab and enter **plugin name** given by the [LoginRadius support team](mailto:support@loginradius.com) then click **Sign in** button and you will be redirected to the Azure AD page for login.</span><span class="sxs-lookup"><span data-stu-id="d7774-159">Click on **Single Sign-On** tab and enter **plugin name** given by the [LoginRadius support team](mailto:support@loginradius.com) then click **Sign in** button and you will be redirected to the Azure AD page for login.</span></span> 

1. <span data-ttu-id="d7774-160">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d7774-160">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/lr-tutorial/tutorial_LoginRadius_certificate.png) 

1. <span data-ttu-id="d7774-162">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="d7774-162">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/lr-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="d7774-164">To configure single sign-on on **LoginRadius** side, you need to send the downloaded **Metadata XML** to [LoginRadius support team](mailto:support@loginradius.com).</span><span class="sxs-lookup"><span data-stu-id="d7774-164">To configure single sign-on on **LoginRadius** side, you need to send the downloaded **Metadata XML** to [LoginRadius support team](mailto:support@loginradius.com).</span></span> <span data-ttu-id="d7774-165">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="d7774-165">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d7774-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="d7774-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d7774-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="d7774-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d7774-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d7774-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d7774-169">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d7774-169">Create an Azure AD test user</span></span>

<span data-ttu-id="d7774-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d7774-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="d7774-172">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d7774-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d7774-173">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="d7774-173">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/lr-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="d7774-175">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="d7774-175">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/lr-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="d7774-177">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="d7774-177">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/lr-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="d7774-179">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d7774-179">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/lr-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d7774-181">a.</span><span class="sxs-lookup"><span data-stu-id="d7774-181">a.</span></span> <span data-ttu-id="d7774-182">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d7774-182">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d7774-183">b.</span><span class="sxs-lookup"><span data-stu-id="d7774-183">b.</span></span> <span data-ttu-id="d7774-184">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d7774-184">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="d7774-185">c.</span><span class="sxs-lookup"><span data-stu-id="d7774-185">c.</span></span> <span data-ttu-id="d7774-186">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="d7774-186">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="d7774-187">d.</span><span class="sxs-lookup"><span data-stu-id="d7774-187">d.</span></span> <span data-ttu-id="d7774-188">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d7774-188">Click **Create**.</span></span>
 
### <a name="create-a-loginradius-test-user"></a><span data-ttu-id="d7774-189">Create a LoginRadius test user</span><span class="sxs-lookup"><span data-stu-id="d7774-189">Create a LoginRadius test user</span></span>

<span data-ttu-id="d7774-190">In this section, you create a user called Britta Simon in LoginRadius.</span><span class="sxs-lookup"><span data-stu-id="d7774-190">In this section, you create a user called Britta Simon in LoginRadius.</span></span> <span data-ttu-id="d7774-191">Work with [LoginRadius support team](mailto:support@loginradius.com) to add the users in the LoginRadius platform.</span><span class="sxs-lookup"><span data-stu-id="d7774-191">Work with [LoginRadius support team](mailto:support@loginradius.com) to add the users in the LoginRadius platform.</span></span> <span data-ttu-id="d7774-192">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d7774-192">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d7774-193">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d7774-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="d7774-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LoginRadius.</span><span class="sxs-lookup"><span data-stu-id="d7774-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LoginRadius.</span></span>

![Assign the user role][200] 

<span data-ttu-id="d7774-196">**To assign Britta Simon to LoginRadius, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d7774-196">**To assign Britta Simon to LoginRadius, perform the following steps:**</span></span>

1. <span data-ttu-id="d7774-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d7774-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="d7774-199">In the applications list, select **LoginRadius**.</span><span class="sxs-lookup"><span data-stu-id="d7774-199">In the applications list, select **LoginRadius**.</span></span>

    ![The LoginRadius link in the Applications list](./media/lr-tutorial/tutorial_LoginRadius_app.png)  

1. <span data-ttu-id="d7774-201">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="d7774-201">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="d7774-203">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="d7774-203">Click **Add** button.</span></span> <span data-ttu-id="d7774-204">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d7774-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="d7774-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="d7774-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="d7774-207">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="d7774-207">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="d7774-208">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d7774-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d7774-209">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="d7774-209">Test single sign-on</span></span>

<span data-ttu-id="d7774-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d7774-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d7774-211">When you click the LoginRadius tile in the Access Panel, you should get automatically signed-on to your LoginRadius application.</span><span class="sxs-lookup"><span data-stu-id="d7774-211">When you click the LoginRadius tile in the Access Panel, you should get automatically signed-on to your LoginRadius application.</span></span>
<span data-ttu-id="d7774-212">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d7774-212">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d7774-213">Additional resources</span><span class="sxs-lookup"><span data-stu-id="d7774-213">Additional resources</span></span>

* [<span data-ttu-id="d7774-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d7774-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="d7774-215">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d7774-215">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/lr-tutorial/tutorial_general_01.png
[2]: ./media/lr-tutorial/tutorial_general_02.png
[3]: ./media/lr-tutorial/tutorial_general_03.png
[4]: ./media/lr-tutorial/tutorial_general_04.png

[100]: ./media/lr-tutorial/tutorial_general_100.png

[200]: ./media/lr-tutorial/tutorial_general_200.png
[201]: ./media/lr-tutorial/tutorial_general_201.png
[202]: ./media/lr-tutorial/tutorial_general_202.png
[203]: ./media/lr-tutorial/tutorial_general_203.png

