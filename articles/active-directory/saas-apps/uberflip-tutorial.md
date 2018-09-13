---
title: 'Tutorial: Azure Active Directory integration with Uberflip | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Uberflip.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 754b1f5b-6694-4fd6-9e1e-9fad769c64db
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2018
ms.author: jeedes
ms.openlocfilehash: bb1f53895fcd91a9474302fcf8c9e0040fe91961
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857533"
---
# <a name="tutorial-azure-active-directory-integration-with-uberflip"></a><span data-ttu-id="54863-103">Tutorial: Azure Active Directory integration with Uberflip</span><span class="sxs-lookup"><span data-stu-id="54863-103">Tutorial: Azure Active Directory integration with Uberflip</span></span>

<span data-ttu-id="54863-104">In this tutorial, you learn how to integrate Uberflip with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="54863-104">In this tutorial, you learn how to integrate Uberflip with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="54863-105">Integrating Uberflip with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="54863-105">Integrating Uberflip with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="54863-106">You can control in Azure AD who has access to Uberflip.</span><span class="sxs-lookup"><span data-stu-id="54863-106">You can control in Azure AD who has access to Uberflip.</span></span>
- <span data-ttu-id="54863-107">You can enable your users to automatically get signed-on to Uberflip (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="54863-107">You can enable your users to automatically get signed-on to Uberflip (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="54863-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="54863-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="54863-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span><span class="sxs-lookup"><span data-stu-id="54863-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54863-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="54863-110">Prerequisites</span></span>

<span data-ttu-id="54863-111">To configure Azure AD integration with Uberflip, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="54863-111">To configure Azure AD integration with Uberflip, you need the following items:</span></span>

- <span data-ttu-id="54863-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="54863-112">An Azure AD subscription</span></span>
- <span data-ttu-id="54863-113">A Uberflip single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="54863-113">A Uberflip single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="54863-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="54863-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="54863-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="54863-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="54863-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="54863-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="54863-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="54863-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="54863-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="54863-118">Scenario description</span></span>

<span data-ttu-id="54863-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="54863-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="54863-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="54863-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="54863-121">Adding Uberflip from the gallery</span><span class="sxs-lookup"><span data-stu-id="54863-121">Adding Uberflip from the gallery</span></span>
2. <span data-ttu-id="54863-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="54863-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-uberflip-from-the-gallery"></a><span data-ttu-id="54863-123">Adding Uberflip from the gallery</span><span class="sxs-lookup"><span data-stu-id="54863-123">Adding Uberflip from the gallery</span></span>

<span data-ttu-id="54863-124">To configure the integration of Uberflip into Azure AD, you need to add Uberflip from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="54863-124">To configure the integration of Uberflip into Azure AD, you need to add Uberflip from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="54863-125">**To add Uberflip from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54863-125">**To add Uberflip from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="54863-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="54863-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="54863-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="54863-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="54863-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="54863-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="54863-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="54863-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="54863-133">In the search box, type **Uberflip**, select **Uberflip** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="54863-133">In the search box, type **Uberflip**, select **Uberflip** from result panel then click **Add** button to add the application.</span></span>

    ![Uberflip in the results list](./media/uberflip-tutorial/tutorial_uberflip_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="54863-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="54863-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="54863-136">In this section, you configure and test Azure AD single sign-on with Uberflip based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="54863-136">In this section, you configure and test Azure AD single sign-on with Uberflip based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="54863-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Uberflip is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54863-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Uberflip is to a user in Azure AD.</span></span> <span data-ttu-id="54863-138">In other words, a link relationship between an Azure AD user and the related user in Uberflip needs to be established.</span><span class="sxs-lookup"><span data-stu-id="54863-138">In other words, a link relationship between an Azure AD user and the related user in Uberflip needs to be established.</span></span>

<span data-ttu-id="54863-139">To configure and test Azure AD single sign-on with Uberflip, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="54863-139">To configure and test Azure AD single sign-on with Uberflip, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="54863-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="54863-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="54863-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54863-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="54863-142">**[Create an Uberflip test user](#create-an-uberflip-test-user)** - to have a counterpart of Britta Simon in Uberflip that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="54863-142">**[Create an Uberflip test user](#create-an-uberflip-test-user)** - to have a counterpart of Britta Simon in Uberflip that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="54863-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="54863-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="54863-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="54863-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="54863-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="54863-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="54863-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Uberflip application.</span><span class="sxs-lookup"><span data-stu-id="54863-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Uberflip application.</span></span>

<span data-ttu-id="54863-147">**To configure Azure AD single sign-on with Uberflip, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54863-147">**To configure Azure AD single sign-on with Uberflip, perform the following steps:**</span></span>

1. <span data-ttu-id="54863-148">In the Azure portal, on the **Uberflip** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="54863-148">In the Azure portal, on the **Uberflip** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="54863-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="54863-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/uberflip-tutorial/tutorial_uberflip_samlbase.png)

3. <span data-ttu-id="54863-152">On the **Uberflip Domain and URLs** section, perform the following step if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="54863-152">On the **Uberflip Domain and URLs** section, perform the following step if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Uberflip Domain and URLs single sign-on information](./media/uberflip-tutorial/tutorial_uberflip_url1.png)

    <span data-ttu-id="54863-154">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.uberflip.com/sso/saml2/<IDPID>/<ACCOUNTID>`</span><span class="sxs-lookup"><span data-stu-id="54863-154">In the **Reply URL** textbox, type a URL using the following pattern: `https://app.uberflip.com/sso/saml2/<IDPID>/<ACCOUNTID>`</span></span>

    > [!NOTE]
    > <span data-ttu-id="54863-155">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="54863-155">This value is not real.</span></span> <span data-ttu-id="54863-156">Update this value with the actual Reply URL.</span><span class="sxs-lookup"><span data-stu-id="54863-156">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="54863-157">Contact [Uberflip Client support team](mailto:support@uberflip.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="54863-157">Contact [Uberflip Client support team](mailto:support@uberflip.com) to get this value.</span></span>

4. <span data-ttu-id="54863-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="54863-158">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Uberflip Domain and URLs single sign-on information](./media/uberflip-tutorial/tutorial_uberflip_url2.png)

    <span data-ttu-id="54863-160">In the **Sign-on URL** textbox, type the URL: `https://app.uberflip.com/users/login`</span><span class="sxs-lookup"><span data-stu-id="54863-160">In the **Sign-on URL** textbox, type the URL: `https://app.uberflip.com/users/login`</span></span>

5. <span data-ttu-id="54863-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="54863-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/uberflip-tutorial/tutorial_uberflip_certificate.png) 

6. <span data-ttu-id="54863-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="54863-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/uberflip-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="54863-165">To configure single sign-on on **Uberflip** side, you need to send the downloaded **Metadata XML** to [Uberflip support team](mailto:support@uberflip.com).</span><span class="sxs-lookup"><span data-stu-id="54863-165">To configure single sign-on on **Uberflip** side, you need to send the downloaded **Metadata XML** to [Uberflip support team](mailto:support@uberflip.com).</span></span> <span data-ttu-id="54863-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="54863-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="54863-167">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="54863-167">Create an Azure AD test user</span></span>

<span data-ttu-id="54863-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54863-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="54863-170">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54863-170">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="54863-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="54863-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/uberflip-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="54863-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="54863-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/uberflip-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="54863-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="54863-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/uberflip-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="54863-177">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="54863-177">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/uberflip-tutorial/create_aaduser_04.png)

    <span data-ttu-id="54863-179">a.</span><span class="sxs-lookup"><span data-stu-id="54863-179">a.</span></span> <span data-ttu-id="54863-180">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="54863-180">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="54863-181">b.</span><span class="sxs-lookup"><span data-stu-id="54863-181">b.</span></span> <span data-ttu-id="54863-182">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54863-182">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="54863-183">c.</span><span class="sxs-lookup"><span data-stu-id="54863-183">c.</span></span> <span data-ttu-id="54863-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="54863-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="54863-185">d.</span><span class="sxs-lookup"><span data-stu-id="54863-185">d.</span></span> <span data-ttu-id="54863-186">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="54863-186">Click **Create**.</span></span>

### <a name="create-an-uberflip-test-user"></a><span data-ttu-id="54863-187">Create an Uberflip test user</span><span class="sxs-lookup"><span data-stu-id="54863-187">Create an Uberflip test user</span></span>

<span data-ttu-id="54863-188">The objective of this section is to create a user called Britta Simon in Uberflip.</span><span class="sxs-lookup"><span data-stu-id="54863-188">The objective of this section is to create a user called Britta Simon in Uberflip.</span></span> <span data-ttu-id="54863-189">Uberflip supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="54863-189">Uberflip supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="54863-190">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="54863-190">There is no action item for you in this section.</span></span> <span data-ttu-id="54863-191">A new user is created during an attempt to access Uberflip if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="54863-191">A new user is created during an attempt to access Uberflip if it doesn't exist yet.</span></span>

> [!Note]
> <span data-ttu-id="54863-192">If you need to create a user manually, contact [Uberflip support team](mailto:support@uberflip.com).</span><span class="sxs-lookup"><span data-stu-id="54863-192">If you need to create a user manually, contact [Uberflip support team](mailto:support@uberflip.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="54863-193">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="54863-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="54863-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Uberflip.</span><span class="sxs-lookup"><span data-stu-id="54863-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Uberflip.</span></span>

![Assign the user role][200] 

<span data-ttu-id="54863-196">**To assign Britta Simon to Uberflip, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="54863-196">**To assign Britta Simon to Uberflip, perform the following steps:**</span></span>

1. <span data-ttu-id="54863-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="54863-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="54863-199">In the applications list, select **Uberflip**.</span><span class="sxs-lookup"><span data-stu-id="54863-199">In the applications list, select **Uberflip**.</span></span>

    ![The Uberflip link in the Applications list](./media/uberflip-tutorial/tutorial_uberflip_app.png)  

3. <span data-ttu-id="54863-201">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="54863-201">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="54863-203">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="54863-203">Click **Add** button.</span></span> <span data-ttu-id="54863-204">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="54863-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="54863-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="54863-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="54863-207">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="54863-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="54863-208">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="54863-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="54863-209">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="54863-209">Test single sign-on</span></span>

<span data-ttu-id="54863-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="54863-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="54863-211">When you click the Uberflip tile in the Access Panel, you should get automatically signed-on to your Uberflip application.</span><span class="sxs-lookup"><span data-stu-id="54863-211">When you click the Uberflip tile in the Access Panel, you should get automatically signed-on to your Uberflip application.</span></span>
<span data-ttu-id="54863-212">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="54863-212">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="54863-213">Additional resources</span><span class="sxs-lookup"><span data-stu-id="54863-213">Additional resources</span></span>

* [<span data-ttu-id="54863-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="54863-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="54863-215">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="54863-215">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/uberflip-tutorial/tutorial_general_01.png
[2]: ./media/uberflip-tutorial/tutorial_general_02.png
[3]: ./media/uberflip-tutorial/tutorial_general_03.png
[4]: ./media/uberflip-tutorial/tutorial_general_04.png

[100]: ./media/uberflip-tutorial/tutorial_general_100.png

[200]: ./media/uberflip-tutorial/tutorial_general_200.png
[201]: ./media/uberflip-tutorial/tutorial_general_201.png
[202]: ./media/uberflip-tutorial/tutorial_general_202.png
[203]: ./media/uberflip-tutorial/tutorial_general_203.png