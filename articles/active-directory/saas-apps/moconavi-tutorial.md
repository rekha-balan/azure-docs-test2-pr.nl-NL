---
title: 'Tutorial: Azure Active Directory integration with moconavi | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and moconavi.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e1916224-e1c2-426f-b233-0a2518fa41db
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2018
ms.author: jeedes
ms.openlocfilehash: 3467b823e6c91d34ebd48c7f8bc29558a79c59e5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868696"
---
# <a name="tutorial-azure-active-directory-integration-with-moconavi"></a><span data-ttu-id="4c203-103">Tutorial: Azure Active Directory integration with moconavi</span><span class="sxs-lookup"><span data-stu-id="4c203-103">Tutorial: Azure Active Directory integration with moconavi</span></span>

<span data-ttu-id="4c203-104">In this tutorial, you learn how to integrate moconavi with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4c203-104">In this tutorial, you learn how to integrate moconavi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4c203-105">Integrating moconavi with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="4c203-105">Integrating moconavi with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4c203-106">You can control in Azure AD who has access to moconavi.</span><span class="sxs-lookup"><span data-stu-id="4c203-106">You can control in Azure AD who has access to moconavi.</span></span>
- <span data-ttu-id="4c203-107">You can enable your users to automatically get signed-on to moconavi (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="4c203-107">You can enable your users to automatically get signed-on to moconavi (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4c203-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4c203-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="4c203-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="4c203-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c203-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4c203-110">Prerequisites</span></span>

<span data-ttu-id="4c203-111">To configure Azure AD integration with moconavi, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="4c203-111">To configure Azure AD integration with moconavi, you need the following items:</span></span>

- <span data-ttu-id="4c203-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="4c203-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4c203-113">A moconavi single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="4c203-113">A moconavi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4c203-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="4c203-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4c203-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="4c203-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4c203-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="4c203-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4c203-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c203-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4c203-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="4c203-118">Scenario description</span></span>
<span data-ttu-id="4c203-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="4c203-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>
<span data-ttu-id="4c203-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="4c203-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4c203-121">Adding moconavi from the gallery</span><span class="sxs-lookup"><span data-stu-id="4c203-121">Adding moconavi from the gallery</span></span>
2. <span data-ttu-id="4c203-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4c203-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moconavi-from-the-gallery"></a><span data-ttu-id="4c203-123">Adding moconavi from the gallery</span><span class="sxs-lookup"><span data-stu-id="4c203-123">Adding moconavi from the gallery</span></span>
<span data-ttu-id="4c203-124">To configure the integration of moconavi into Azure AD, you need to add moconavi from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="4c203-124">To configure the integration of moconavi into Azure AD, you need to add moconavi from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4c203-125">**To add moconavi from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4c203-125">**To add moconavi from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4c203-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="4c203-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="4c203-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="4c203-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4c203-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4c203-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="4c203-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="4c203-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="4c203-133">In the search box, type **moconavi**, select **moconavi** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="4c203-133">In the search box, type **moconavi**, select **moconavi** from result panel then click **Add** button to add the application.</span></span>

    ![moconavi in the results list](./media/moconavi-tutorial/tutorial_moconavi_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4c203-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4c203-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4c203-136">In this section, you configure and test Azure AD single sign-on with moconavi based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="4c203-136">In this section, you configure and test Azure AD single sign-on with moconavi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4c203-137">For single sign-on to work, Azure AD needs to know what the counterpart user in moconavi is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c203-137">For single sign-on to work, Azure AD needs to know what the counterpart user in moconavi is to a user in Azure AD.</span></span> <span data-ttu-id="4c203-138">In other words, a link relationship between an Azure AD user and the related user in moconavi needs to be established.</span><span class="sxs-lookup"><span data-stu-id="4c203-138">In other words, a link relationship between an Azure AD user and the related user in moconavi needs to be established.</span></span>

<span data-ttu-id="4c203-139">To configure and test Azure AD single sign-on with moconavi, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="4c203-139">To configure and test Azure AD single sign-on with moconavi, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4c203-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="4c203-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4c203-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c203-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4c203-142">**[Create a moconavi test user](#create-a-moconavi-test-user)** - to have a counterpart of Britta Simon in moconavi that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="4c203-142">**[Create a moconavi test user](#create-a-moconavi-test-user)** - to have a counterpart of Britta Simon in moconavi that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4c203-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4c203-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4c203-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="4c203-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4c203-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="4c203-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4c203-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your moconavi application.</span><span class="sxs-lookup"><span data-stu-id="4c203-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your moconavi application.</span></span>

<span data-ttu-id="4c203-147">**To configure Azure AD single sign-on with moconavi, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4c203-147">**To configure Azure AD single sign-on with moconavi, perform the following steps:**</span></span>

1. <span data-ttu-id="4c203-148">In the Azure portal, on the **moconavi** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="4c203-148">In the Azure portal, on the **moconavi** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="4c203-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4c203-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/moconavi-tutorial/tutorial_moconavi_samlbase.png)

3. <span data-ttu-id="4c203-152">On the **moconavi Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4c203-152">On the **moconavi Domain and URLs** section, perform the following steps:</span></span>

    ![moconavi Domain and URLs single sign-on information](./media/moconavi-tutorial/tutorial_moconavi_url.png)

    <span data-ttu-id="4c203-154">a.</span><span class="sxs-lookup"><span data-stu-id="4c203-154">a.</span></span> <span data-ttu-id="4c203-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<yourserverurl>/moconavi-saml2/saml/login`</span><span class="sxs-lookup"><span data-stu-id="4c203-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<yourserverurl>/moconavi-saml2/saml/login`</span></span>

    <span data-ttu-id="4c203-156">b.</span><span class="sxs-lookup"><span data-stu-id="4c203-156">b.</span></span> <span data-ttu-id="4c203-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<yourserverurl>/moconavi-saml2`</span><span class="sxs-lookup"><span data-stu-id="4c203-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<yourserverurl>/moconavi-saml2`</span></span>

    <span data-ttu-id="4c203-158">C.</span><span class="sxs-lookup"><span data-stu-id="4c203-158">C.</span></span> <span data-ttu-id="4c203-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<yourserverurl>/moconavi-saml2/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="4c203-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<yourserverurl>/moconavi-saml2/saml/SSO`</span></span>

    > [!NOTE]
    > <span data-ttu-id="4c203-160">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="4c203-160">These values are not real.</span></span> <span data-ttu-id="4c203-161">Update these values with the actual Sign-On URL, Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="4c203-161">Update these values with the actual Sign-On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="4c203-162">Contact [moconavi Client support team](mailto:support@recomot.co.jp) to get these values.</span><span class="sxs-lookup"><span data-stu-id="4c203-162">Contact [moconavi Client support team](mailto:support@recomot.co.jp) to get these values.</span></span>

4. <span data-ttu-id="4c203-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="4c203-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/moconavi-tutorial/tutorial_moconavi_certificate.png)

5. <span data-ttu-id="4c203-165">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="4c203-165">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/moconavi-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4c203-167">To configure single sign-on on **moconavi** side, you need to send the downloaded **Metadata XML** to [moconavi support team](mailto:support@recomot.co.jp).</span><span class="sxs-lookup"><span data-stu-id="4c203-167">To configure single sign-on on **moconavi** side, you need to send the downloaded **Metadata XML** to [moconavi support team](mailto:support@recomot.co.jp).</span></span> <span data-ttu-id="4c203-168">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="4c203-168">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4c203-169">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4c203-169">Create an Azure AD test user</span></span>

<span data-ttu-id="4c203-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c203-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="4c203-172">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4c203-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4c203-173">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="4c203-173">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/moconavi-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4c203-175">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="4c203-175">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/moconavi-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4c203-177">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="4c203-177">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/moconavi-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4c203-179">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4c203-179">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/moconavi-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4c203-181">a.</span><span class="sxs-lookup"><span data-stu-id="4c203-181">a.</span></span> <span data-ttu-id="4c203-182">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4c203-182">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4c203-183">b.</span><span class="sxs-lookup"><span data-stu-id="4c203-183">b.</span></span> <span data-ttu-id="4c203-184">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c203-184">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="4c203-185">c.</span><span class="sxs-lookup"><span data-stu-id="4c203-185">c.</span></span> <span data-ttu-id="4c203-186">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="4c203-186">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="4c203-187">d.</span><span class="sxs-lookup"><span data-stu-id="4c203-187">d.</span></span> <span data-ttu-id="4c203-188">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="4c203-188">Click **Create**.</span></span>

### <a name="create-a-moconavi-test-user"></a><span data-ttu-id="4c203-189">Create a moconavi test user</span><span class="sxs-lookup"><span data-stu-id="4c203-189">Create a moconavi test user</span></span>

<span data-ttu-id="4c203-190">In this section, you create a user called Britta Simon in moconavi.</span><span class="sxs-lookup"><span data-stu-id="4c203-190">In this section, you create a user called Britta Simon in moconavi.</span></span> <span data-ttu-id="4c203-191">Work with [moconavi support team](mailto:support@recomot.co.jp) to add the users in the moconavi platform.</span><span class="sxs-lookup"><span data-stu-id="4c203-191">Work with [moconavi support team](mailto:support@recomot.co.jp) to add the users in the moconavi platform.</span></span> <span data-ttu-id="4c203-192">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="4c203-192">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4c203-193">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="4c203-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="4c203-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to moconavi.</span><span class="sxs-lookup"><span data-stu-id="4c203-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to moconavi.</span></span>

![Assign the user role][200]

<span data-ttu-id="4c203-196">**To assign Britta Simon to moconavi, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="4c203-196">**To assign Britta Simon to moconavi, perform the following steps:**</span></span>

1. <span data-ttu-id="4c203-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="4c203-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="4c203-199">In the applications list, select **moconavi**.</span><span class="sxs-lookup"><span data-stu-id="4c203-199">In the applications list, select **moconavi**.</span></span>

    ![The moconavi link in the Applications list](./media/moconavi-tutorial/tutorial_moconavi_app.png)

3. <span data-ttu-id="4c203-201">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="4c203-201">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="4c203-203">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="4c203-203">Click **Add** button.</span></span> <span data-ttu-id="4c203-204">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4c203-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="4c203-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="4c203-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4c203-207">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="4c203-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4c203-208">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="4c203-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="4c203-209">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="4c203-209">Test single sign-on</span></span>

1. <span data-ttu-id="4c203-210">Install moconavi from Microsoft store.</span><span class="sxs-lookup"><span data-stu-id="4c203-210">Install moconavi from Microsoft store.</span></span>

2. <span data-ttu-id="4c203-211">Start moconavi.</span><span class="sxs-lookup"><span data-stu-id="4c203-211">Start moconavi.</span></span>

3. <span data-ttu-id="4c203-212">Click **Connect setting** button.</span><span class="sxs-lookup"><span data-stu-id="4c203-212">Click **Connect setting** button.</span></span>

    ![Testing single sign-on](./media/moconavi-tutorial/testing1.png)

4. <span data-ttu-id="4c203-214">Enter `https://mcs-admin.moconavi.biz/gateway` into **Connect to URL** textbox and then click **Done** button.</span><span class="sxs-lookup"><span data-stu-id="4c203-214">Enter `https://mcs-admin.moconavi.biz/gateway` into **Connect to URL** textbox and then click **Done** button.</span></span>

    ![Testing single sign-on](./media/moconavi-tutorial/testing2.png)

5. <span data-ttu-id="4c203-216">On the following screenshot, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="4c203-216">On the following screenshot, perform the following steps:</span></span>

    ![Testing single sign-on](./media/moconavi-tutorial/testing3.png)

    <span data-ttu-id="4c203-218">a.</span><span class="sxs-lookup"><span data-stu-id="4c203-218">a.</span></span> <span data-ttu-id="4c203-219">Enter **Input Authentication Key**:`azureAD` into **Input Authentication Key** textbox.</span><span class="sxs-lookup"><span data-stu-id="4c203-219">Enter **Input Authentication Key**:`azureAD` into **Input Authentication Key** textbox.</span></span>

    <span data-ttu-id="4c203-220">b.</span><span class="sxs-lookup"><span data-stu-id="4c203-220">b.</span></span> <span data-ttu-id="4c203-221">Enter **Input User ID**: `your ad account` into **Input User ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="4c203-221">Enter **Input User ID**: `your ad account` into **Input User ID** textbox.</span></span>

    <span data-ttu-id="4c203-222">c.</span><span class="sxs-lookup"><span data-stu-id="4c203-222">c.</span></span> <span data-ttu-id="4c203-223">Click **LOGIN**.</span><span class="sxs-lookup"><span data-stu-id="4c203-223">Click **LOGIN**.</span></span>

6. <span data-ttu-id="4c203-224">Input your Azure AD password to **Password** textbox and then click **Login** button.</span><span class="sxs-lookup"><span data-stu-id="4c203-224">Input your Azure AD password to **Password** textbox and then click **Login** button.</span></span>

    ![Testing single sign-on](./media/moconavi-tutorial/testing4.png)

7. <span data-ttu-id="4c203-226">Azure AD authentication is successful when the menu is displayed.</span><span class="sxs-lookup"><span data-stu-id="4c203-226">Azure AD authentication is successful when the menu is displayed.</span></span>

    ![Testing single sign-on](./media/moconavi-tutorial/testing5.png)

## <a name="additional-resources"></a><span data-ttu-id="4c203-228">Additional resources</span><span class="sxs-lookup"><span data-stu-id="4c203-228">Additional resources</span></span>

* [<span data-ttu-id="4c203-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4c203-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="4c203-230">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4c203-230">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/moconavi-tutorial/tutorial_general_01.png
[2]: ./media/moconavi-tutorial/tutorial_general_02.png
[3]: ./media/moconavi-tutorial/tutorial_general_03.png
[4]: ./media/moconavi-tutorial/tutorial_general_04.png

[100]: ./media/moconavi-tutorial/tutorial_general_100.png

[200]: ./media/moconavi-tutorial/tutorial_general_200.png
[201]: ./media/moconavi-tutorial/tutorial_general_201.png
[202]: ./media/moconavi-tutorial/tutorial_general_202.png
[203]: ./media/moconavi-tutorial/tutorial_general_203.png

