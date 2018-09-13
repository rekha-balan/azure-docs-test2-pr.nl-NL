---
title: 'Tutorial: Azure Active Directory integration with Silverback | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Silverback.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 32cfc96f-2137-49ff-818b-67feadcd73b7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2018
ms.author: jeedes
ms.openlocfilehash: e100859a184db2b6298dd02a1bb7bb238de27d51
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857530"
---
# <a name="tutorial-azure-active-directory-integration-with-silverback"></a><span data-ttu-id="7991d-103">Tutorial: Azure Active Directory integration with Silverback</span><span class="sxs-lookup"><span data-stu-id="7991d-103">Tutorial: Azure Active Directory integration with Silverback</span></span>

<span data-ttu-id="7991d-104">In this tutorial, you learn how to integrate Silverback with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7991d-104">In this tutorial, you learn how to integrate Silverback with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7991d-105">Integrating Silverback with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7991d-105">Integrating Silverback with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7991d-106">You can control in Azure AD who has access to Silverback.</span><span class="sxs-lookup"><span data-stu-id="7991d-106">You can control in Azure AD who has access to Silverback.</span></span>
- <span data-ttu-id="7991d-107">You can enable your users to automatically get signed-on to Silverback (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="7991d-107">You can enable your users to automatically get signed-on to Silverback (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7991d-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7991d-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="7991d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="7991d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7991d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7991d-110">Prerequisites</span></span>

<span data-ttu-id="7991d-111">To configure Azure AD integration with Silverback, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7991d-111">To configure Azure AD integration with Silverback, you need the following items:</span></span>

- <span data-ttu-id="7991d-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7991d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7991d-113">A Silverback single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7991d-113">A Silverback single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7991d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7991d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7991d-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7991d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7991d-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="7991d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7991d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7991d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7991d-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7991d-118">Scenario description</span></span>
<span data-ttu-id="7991d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7991d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7991d-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7991d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7991d-121">Adding Silverback from the gallery</span><span class="sxs-lookup"><span data-stu-id="7991d-121">Adding Silverback from the gallery</span></span>
2. <span data-ttu-id="7991d-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7991d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-silverback-from-the-gallery"></a><span data-ttu-id="7991d-123">Adding Silverback from the gallery</span><span class="sxs-lookup"><span data-stu-id="7991d-123">Adding Silverback from the gallery</span></span>
<span data-ttu-id="7991d-124">To configure the integration of Silverback into Azure AD, you need to add Silverback from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7991d-124">To configure the integration of Silverback into Azure AD, you need to add Silverback from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7991d-125">**To add Silverback from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7991d-125">**To add Silverback from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7991d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="7991d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="7991d-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="7991d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7991d-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7991d-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="7991d-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="7991d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="7991d-133">In the search box, type **Silverback**, select **Silverback** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="7991d-133">In the search box, type **Silverback**, select **Silverback** from result panel then click **Add** button to add the application.</span></span>

    ![Silverback in the results list](./media/silverback-tutorial/tutorial_silverback_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7991d-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7991d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7991d-136">In this section, you configure and test Azure AD single sign-on with Silverback based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7991d-136">In this section, you configure and test Azure AD single sign-on with Silverback based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7991d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Silverback is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7991d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Silverback is to a user in Azure AD.</span></span> <span data-ttu-id="7991d-138">In other words, a link relationship between an Azure AD user and the related user in Silverback needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7991d-138">In other words, a link relationship between an Azure AD user and the related user in Silverback needs to be established.</span></span>

<span data-ttu-id="7991d-139">To configure and test Azure AD single sign-on with Silverback, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7991d-139">To configure and test Azure AD single sign-on with Silverback, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7991d-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7991d-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7991d-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7991d-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7991d-142">**[Create a Silverback test user](#create-a-silverback-test-user)** - to have a counterpart of Britta Simon in Silverback that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="7991d-142">**[Create a Silverback test user](#create-a-silverback-test-user)** - to have a counterpart of Britta Simon in Silverback that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7991d-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7991d-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7991d-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7991d-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7991d-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7991d-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7991d-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Silverback application.</span><span class="sxs-lookup"><span data-stu-id="7991d-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Silverback application.</span></span>

<span data-ttu-id="7991d-147">**To configure Azure AD single sign-on with Silverback, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7991d-147">**To configure Azure AD single sign-on with Silverback, perform the following steps:**</span></span>

1. <span data-ttu-id="7991d-148">In the Azure portal, on the **Silverback** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="7991d-148">In the Azure portal, on the **Silverback** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="7991d-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7991d-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/silverback-tutorial/tutorial_silverback_samlbase.png)

3. <span data-ttu-id="7991d-152">On the **Silverback Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7991d-152">On the **Silverback Domain and URLs** section, perform the following steps:</span></span>

    ![Silverback Domain and URLs single sign-on information](./media/silverback-tutorial/tutorial_silverback_url.png)

    <span data-ttu-id="7991d-154">a.</span><span class="sxs-lookup"><span data-stu-id="7991d-154">a.</span></span> <span data-ttu-id="7991d-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<YOURSILVERBACKURL>/ssp`</span><span class="sxs-lookup"><span data-stu-id="7991d-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<YOURSILVERBACKURL>/ssp`</span></span>

    <span data-ttu-id="7991d-156">b.</span><span class="sxs-lookup"><span data-stu-id="7991d-156">b.</span></span> <span data-ttu-id="7991d-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<YOURSILVERBACKURL>`</span><span class="sxs-lookup"><span data-stu-id="7991d-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<YOURSILVERBACKURL>`</span></span>

    <span data-ttu-id="7991d-158">c.</span><span class="sxs-lookup"><span data-stu-id="7991d-158">c.</span></span> <span data-ttu-id="7991d-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<YOURSILVERBACKURL>/sts/authorize/login`</span><span class="sxs-lookup"><span data-stu-id="7991d-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<YOURSILVERBACKURL>/sts/authorize/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7991d-160">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="7991d-160">These values are not real.</span></span> <span data-ttu-id="7991d-161">Update these values with the actual Sign-On URL, Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="7991d-161">Update these values with the actual Sign-On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="7991d-162">Contact [Silverback Client support team](mailto:helpdesk@matrix42.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="7991d-162">Contact [Silverback Client support team](mailto:helpdesk@matrix42.com) to get these values.</span></span> 

4. <span data-ttu-id="7991d-163">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="7991d-163">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>

    ![The Certificate download link](./media/silverback-tutorial/tutorial_silverback_certificate.png) 

5. <span data-ttu-id="7991d-165">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="7991d-165">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/silverback-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7991d-167">To configure single sign-on on **Silverback** side, you need to send the **App Federation Metadata Url** to [Silverback support team](mailto:helpdesk@matrix42.com).</span><span class="sxs-lookup"><span data-stu-id="7991d-167">To configure single sign-on on **Silverback** side, you need to send the **App Federation Metadata Url** to [Silverback support team](mailto:helpdesk@matrix42.com).</span></span> <span data-ttu-id="7991d-168">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="7991d-168">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7991d-169">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7991d-169">Create an Azure AD test user</span></span>

<span data-ttu-id="7991d-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7991d-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="7991d-172">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7991d-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7991d-173">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="7991d-173">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/silverback-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7991d-175">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="7991d-175">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/silverback-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7991d-177">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="7991d-177">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/silverback-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7991d-179">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7991d-179">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/silverback-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7991d-181">a.</span><span class="sxs-lookup"><span data-stu-id="7991d-181">a.</span></span> <span data-ttu-id="7991d-182">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7991d-182">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7991d-183">b.</span><span class="sxs-lookup"><span data-stu-id="7991d-183">b.</span></span> <span data-ttu-id="7991d-184">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7991d-184">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="7991d-185">c.</span><span class="sxs-lookup"><span data-stu-id="7991d-185">c.</span></span> <span data-ttu-id="7991d-186">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="7991d-186">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="7991d-187">d.</span><span class="sxs-lookup"><span data-stu-id="7991d-187">d.</span></span> <span data-ttu-id="7991d-188">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7991d-188">Click **Create**.</span></span>
 
### <a name="create-a-silverback-test-user"></a><span data-ttu-id="7991d-189">Create a Silverback test user</span><span class="sxs-lookup"><span data-stu-id="7991d-189">Create a Silverback test user</span></span>

<span data-ttu-id="7991d-190">In this section, you create a user called Britta Simon in Silverback.</span><span class="sxs-lookup"><span data-stu-id="7991d-190">In this section, you create a user called Britta Simon in Silverback.</span></span> <span data-ttu-id="7991d-191">Work with [Silverback support team](mailto:helpdesk@matrix42.com) to add the users in the Silverback platform.</span><span class="sxs-lookup"><span data-stu-id="7991d-191">Work with [Silverback support team](mailto:helpdesk@matrix42.com) to add the users in the Silverback platform.</span></span> <span data-ttu-id="7991d-192">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7991d-192">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7991d-193">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7991d-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="7991d-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Silverback.</span><span class="sxs-lookup"><span data-stu-id="7991d-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Silverback.</span></span>

![Assign the user role][200] 

<span data-ttu-id="7991d-196">**To assign Britta Simon to Silverback, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7991d-196">**To assign Britta Simon to Silverback, perform the following steps:**</span></span>

1. <span data-ttu-id="7991d-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="7991d-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="7991d-199">In the applications list, select **Silverback**.</span><span class="sxs-lookup"><span data-stu-id="7991d-199">In the applications list, select **Silverback**.</span></span>

    ![The Silverback link in the Applications list](./media/silverback-tutorial/tutorial_silverback_app.png)  

3. <span data-ttu-id="7991d-201">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="7991d-201">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="7991d-203">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="7991d-203">Click **Add** button.</span></span> <span data-ttu-id="7991d-204">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7991d-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="7991d-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="7991d-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7991d-207">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="7991d-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7991d-208">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="7991d-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7991d-209">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="7991d-209">Test single sign-on</span></span>

<span data-ttu-id="7991d-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7991d-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7991d-211">When you click the Silverback tile in the Access Panel, you should get automatically signed-on to your Silverback application.</span><span class="sxs-lookup"><span data-stu-id="7991d-211">When you click the Silverback tile in the Access Panel, you should get automatically signed-on to your Silverback application.</span></span>
<span data-ttu-id="7991d-212">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7991d-212">For more information about the Access Panel, see [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7991d-213">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7991d-213">Additional resources</span></span>

* [<span data-ttu-id="7991d-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7991d-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="7991d-215">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7991d-215">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/silverback-tutorial/tutorial_general_01.png
[2]: ./media/silverback-tutorial/tutorial_general_02.png
[3]: ./media/silverback-tutorial/tutorial_general_03.png
[4]: ./media/silverback-tutorial/tutorial_general_04.png

[100]: ./media/silverback-tutorial/tutorial_general_100.png

[200]: ./media/silverback-tutorial/tutorial_general_200.png
[201]: ./media/silverback-tutorial/tutorial_general_201.png
[202]: ./media/silverback-tutorial/tutorial_general_202.png
[203]: ./media/silverback-tutorial/tutorial_general_203.png

