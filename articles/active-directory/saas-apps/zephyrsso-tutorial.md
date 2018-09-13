---
title: 'Tutorial: Azure Active Directory integration with ZephyrSSO | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ZephyrSSO.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4d75e26b-c0fa-420b-93c1-e40b68562be8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2018
ms.author: jeedes
ms.openlocfilehash: 47bbdc1c50f0d96f1f26d5595a9e54814fa85188
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866419"
---
# <a name="tutorial-azure-active-directory-integration-with-zephyrsso"></a><span data-ttu-id="0e728-103">Tutorial: Azure Active Directory integration with ZephyrSSO</span><span class="sxs-lookup"><span data-stu-id="0e728-103">Tutorial: Azure Active Directory integration with ZephyrSSO</span></span>

<span data-ttu-id="0e728-104">In this tutorial, you learn how to integrate ZephyrSSO with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0e728-104">In this tutorial, you learn how to integrate ZephyrSSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0e728-105">Integrating ZephyrSSO with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="0e728-105">Integrating ZephyrSSO with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0e728-106">You can control in Azure AD who has access to ZephyrSSO.</span><span class="sxs-lookup"><span data-stu-id="0e728-106">You can control in Azure AD who has access to ZephyrSSO.</span></span>
- <span data-ttu-id="0e728-107">You can enable your users to automatically get signed-on to ZephyrSSO (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="0e728-107">You can enable your users to automatically get signed-on to ZephyrSSO (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0e728-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0e728-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="0e728-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span><span class="sxs-lookup"><span data-stu-id="0e728-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e728-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0e728-110">Prerequisites</span></span>

<span data-ttu-id="0e728-111">To configure Azure AD integration with ZephyrSSO, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="0e728-111">To configure Azure AD integration with ZephyrSSO, you need the following items:</span></span>

- <span data-ttu-id="0e728-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="0e728-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0e728-113">A ZephyrSSO single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="0e728-113">A ZephyrSSO single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0e728-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="0e728-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0e728-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="0e728-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0e728-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="0e728-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0e728-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0e728-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0e728-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="0e728-118">Scenario description</span></span>

<span data-ttu-id="0e728-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="0e728-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0e728-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="0e728-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0e728-121">Adding ZephyrSSO from the gallery</span><span class="sxs-lookup"><span data-stu-id="0e728-121">Adding ZephyrSSO from the gallery</span></span>
2. <span data-ttu-id="0e728-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0e728-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zephyrsso-from-the-gallery"></a><span data-ttu-id="0e728-123">Adding ZephyrSSO from the gallery</span><span class="sxs-lookup"><span data-stu-id="0e728-123">Adding ZephyrSSO from the gallery</span></span>

<span data-ttu-id="0e728-124">To configure the integration of ZephyrSSO into Azure AD, you need to add ZephyrSSO from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="0e728-124">To configure the integration of ZephyrSSO into Azure AD, you need to add ZephyrSSO from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0e728-125">**To add ZephyrSSO from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0e728-125">**To add ZephyrSSO from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0e728-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="0e728-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="0e728-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="0e728-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0e728-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0e728-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="0e728-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="0e728-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="0e728-133">In the search box, type **ZephyrSSO**, select **ZephyrSSO** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="0e728-133">In the search box, type **ZephyrSSO**, select **ZephyrSSO** from result panel then click **Add** button to add the application.</span></span>

    ![ZephyrSSO in the results list](./media/zephyrsso-tutorial/tutorial_zephyrsso_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0e728-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0e728-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0e728-136">In this section, you configure and test Azure AD single sign-on with ZephyrSSO based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0e728-136">In this section, you configure and test Azure AD single sign-on with ZephyrSSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0e728-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ZephyrSSO is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e728-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ZephyrSSO is to a user in Azure AD.</span></span> <span data-ttu-id="0e728-138">In other words, a link relationship between an Azure AD user and the related user in ZephyrSSO needs to be established.</span><span class="sxs-lookup"><span data-stu-id="0e728-138">In other words, a link relationship between an Azure AD user and the related user in ZephyrSSO needs to be established.</span></span>

<span data-ttu-id="0e728-139">To configure and test Azure AD single sign-on with ZephyrSSO, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="0e728-139">To configure and test Azure AD single sign-on with ZephyrSSO, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0e728-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="0e728-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0e728-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0e728-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0e728-142">**[Create a ZephyrSSO test user](#create-a-zephyrsso-test-user)** - to have a counterpart of Britta Simon in ZephyrSSO that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="0e728-142">**[Create a ZephyrSSO test user](#create-a-zephyrsso-test-user)** - to have a counterpart of Britta Simon in ZephyrSSO that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0e728-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0e728-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0e728-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="0e728-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0e728-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0e728-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0e728-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ZephyrSSO application.</span><span class="sxs-lookup"><span data-stu-id="0e728-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ZephyrSSO application.</span></span>

<span data-ttu-id="0e728-147">**To configure Azure AD single sign-on with ZephyrSSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0e728-147">**To configure Azure AD single sign-on with ZephyrSSO, perform the following steps:**</span></span>

1. <span data-ttu-id="0e728-148">In the Azure portal, on the **ZephyrSSO** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="0e728-148">In the Azure portal, on the **ZephyrSSO** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="0e728-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0e728-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/zephyrsso-tutorial/tutorial_zephyrsso_samlbase.png)

3. <span data-ttu-id="0e728-152">On the **ZephyrSSO Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0e728-152">On the **ZephyrSSO Domain and URLs** section, perform the following steps:</span></span>

    ![ZephyrSSO Domain and URLs single sign-on information](./media/zephyrsso-tutorial/tutorial_zephyrsso_url.png)

    <span data-ttu-id="0e728-154">a.</span><span class="sxs-lookup"><span data-stu-id="0e728-154">a.</span></span> <span data-ttu-id="0e728-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.yourzephyr.com/Zephyrsso`</span><span class="sxs-lookup"><span data-stu-id="0e728-155">In the **Identifier** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.yourzephyr.com/Zephyrsso`</span></span>

    <span data-ttu-id="0e728-156">b.</span><span class="sxs-lookup"><span data-stu-id="0e728-156">b.</span></span> <span data-ttu-id="0e728-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.yourzephyr.com/flex/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="0e728-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<SUBDOMAIN>.yourzephyr.com/flex/saml/sso`</span></span>

    > [!NOTE]
    > <span data-ttu-id="0e728-158">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="0e728-158">These values are not real.</span></span> <span data-ttu-id="0e728-159">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="0e728-159">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="0e728-160">Contact [ZephyrSSO support team](https://support.getzephyr.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="0e728-160">Contact [ZephyrSSO support team](https://support.getzephyr.com) to get these values.</span></span>

4. <span data-ttu-id="0e728-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="0e728-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/zephyrsso-tutorial/tutorial_zephyrsso_certificate.png)

5. <span data-ttu-id="0e728-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="0e728-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/zephyrsso-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0e728-165">To configure single sign-on on **ZephyrSSO** side, you need to send the downloaded **Metadata XML** to [ZephyrSSO support team](https://support.getzephyr.com).</span><span class="sxs-lookup"><span data-stu-id="0e728-165">To configure single sign-on on **ZephyrSSO** side, you need to send the downloaded **Metadata XML** to [ZephyrSSO support team](https://support.getzephyr.com).</span></span> <span data-ttu-id="0e728-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="0e728-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0e728-167">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0e728-167">Create an Azure AD test user</span></span>

<span data-ttu-id="0e728-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0e728-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="0e728-170">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0e728-170">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0e728-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="0e728-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/zephyrsso-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="0e728-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="0e728-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/zephyrsso-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="0e728-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="0e728-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/zephyrsso-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="0e728-177">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0e728-177">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/zephyrsso-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0e728-179">a.</span><span class="sxs-lookup"><span data-stu-id="0e728-179">a.</span></span> <span data-ttu-id="0e728-180">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0e728-180">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0e728-181">b.</span><span class="sxs-lookup"><span data-stu-id="0e728-181">b.</span></span> <span data-ttu-id="0e728-182">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0e728-182">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="0e728-183">c.</span><span class="sxs-lookup"><span data-stu-id="0e728-183">c.</span></span> <span data-ttu-id="0e728-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="0e728-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="0e728-185">d.</span><span class="sxs-lookup"><span data-stu-id="0e728-185">d.</span></span> <span data-ttu-id="0e728-186">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0e728-186">Click **Create**.</span></span>
  
### <a name="create-a-zephyrsso-test-user"></a><span data-ttu-id="0e728-187">Create a ZephyrSSO test user</span><span class="sxs-lookup"><span data-stu-id="0e728-187">Create a ZephyrSSO test user</span></span>

<span data-ttu-id="0e728-188">In this section, you create a user called Britta Simon in ZephyrSSO.</span><span class="sxs-lookup"><span data-stu-id="0e728-188">In this section, you create a user called Britta Simon in ZephyrSSO.</span></span> <span data-ttu-id="0e728-189">Work with [ZephyrSSO support team](https://support.getzephyr.com) to add the users in the ZephyrSSO platform.</span><span class="sxs-lookup"><span data-stu-id="0e728-189">Work with [ZephyrSSO support team](https://support.getzephyr.com) to add the users in the ZephyrSSO platform.</span></span> <span data-ttu-id="0e728-190">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0e728-190">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0e728-191">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0e728-191">Assign the Azure AD test user</span></span>

<span data-ttu-id="0e728-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ZephyrSSO.</span><span class="sxs-lookup"><span data-stu-id="0e728-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ZephyrSSO.</span></span>

![Assign the user role][200]

<span data-ttu-id="0e728-194">**To assign Britta Simon to ZephyrSSO, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0e728-194">**To assign Britta Simon to ZephyrSSO, perform the following steps:**</span></span>

1. <span data-ttu-id="0e728-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0e728-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="0e728-197">In the applications list, select **ZephyrSSO**.</span><span class="sxs-lookup"><span data-stu-id="0e728-197">In the applications list, select **ZephyrSSO**.</span></span>

    ![The ZephyrSSO link in the Applications list](./media/zephyrsso-tutorial/tutorial_zephyrsso_app.png)  

3. <span data-ttu-id="0e728-199">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="0e728-199">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="0e728-201">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="0e728-201">Click **Add** button.</span></span> <span data-ttu-id="0e728-202">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0e728-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="0e728-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="0e728-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0e728-205">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="0e728-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0e728-206">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0e728-206">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="0e728-207">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="0e728-207">Test single sign-on</span></span>

<span data-ttu-id="0e728-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="0e728-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0e728-209">When you click the ZephyrSSO tile in the Access Panel, you should get automatically signed-on to your ZephyrSSO application.</span><span class="sxs-lookup"><span data-stu-id="0e728-209">When you click the ZephyrSSO tile in the Access Panel, you should get automatically signed-on to your ZephyrSSO application.</span></span>
<span data-ttu-id="0e728-210">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0e728-210">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0e728-211">Additional resources</span><span class="sxs-lookup"><span data-stu-id="0e728-211">Additional resources</span></span>

* [<span data-ttu-id="0e728-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0e728-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="0e728-213">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0e728-213">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/zephyrsso-tutorial/tutorial_general_01.png
[2]: ./media/zephyrsso-tutorial/tutorial_general_02.png
[3]: ./media/zephyrsso-tutorial/tutorial_general_03.png
[4]: ./media/zephyrsso-tutorial/tutorial_general_04.png

[100]: ./media/zephyrsso-tutorial/tutorial_general_100.png

[200]: ./media/zephyrsso-tutorial/tutorial_general_200.png
[201]: ./media/zephyrsso-tutorial/tutorial_general_201.png
[202]: ./media/zephyrsso-tutorial/tutorial_general_202.png
[203]: ./media/zephyrsso-tutorial/tutorial_general_203.png