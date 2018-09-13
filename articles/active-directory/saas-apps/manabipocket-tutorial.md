---
title: 'Tutorial: Azure Active Directory integration with Manabi Pocket | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Manabi Pocket.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8e521099-bf7d-43ab-a0e0-86aa1c9e577e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2018
ms.author: jeedes
ms.openlocfilehash: 0116cac7d0e44efee0112d57aedd4f5ee02833b3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856162"
---
# <a name="tutorial-azure-active-directory-integration-with-manabi-pocket"></a><span data-ttu-id="8c465-103">Tutorial: Azure Active Directory integration with Manabi Pocket</span><span class="sxs-lookup"><span data-stu-id="8c465-103">Tutorial: Azure Active Directory integration with Manabi Pocket</span></span>

<span data-ttu-id="8c465-104">In this tutorial, you learn how to integrate Manabi Pocket with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8c465-104">In this tutorial, you learn how to integrate Manabi Pocket with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8c465-105">Integrating Manabi Pocket with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8c465-105">Integrating Manabi Pocket with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8c465-106">You can control in Azure AD who has access to Manabi Pocket.</span><span class="sxs-lookup"><span data-stu-id="8c465-106">You can control in Azure AD who has access to Manabi Pocket.</span></span>
- <span data-ttu-id="8c465-107">You can enable your users to automatically get signed-on to Manabi Pocket (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="8c465-107">You can enable your users to automatically get signed-on to Manabi Pocket (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8c465-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8c465-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="8c465-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="8c465-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c465-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8c465-110">Prerequisites</span></span>

<span data-ttu-id="8c465-111">To configure Azure AD integration with Manabi Pocket, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8c465-111">To configure Azure AD integration with Manabi Pocket, you need the following items:</span></span>

- <span data-ttu-id="8c465-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8c465-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8c465-113">A Manabi Pocket single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8c465-113">A Manabi Pocket single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8c465-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8c465-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8c465-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8c465-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8c465-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="8c465-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8c465-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8c465-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8c465-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="8c465-118">Scenario description</span></span>
<span data-ttu-id="8c465-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8c465-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8c465-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8c465-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8c465-121">Adding Manabi Pocket from the gallery</span><span class="sxs-lookup"><span data-stu-id="8c465-121">Adding Manabi Pocket from the gallery</span></span>
1. <span data-ttu-id="8c465-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8c465-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-manabi-pocket-from-the-gallery"></a><span data-ttu-id="8c465-123">Adding Manabi Pocket from the gallery</span><span class="sxs-lookup"><span data-stu-id="8c465-123">Adding Manabi Pocket from the gallery</span></span>
<span data-ttu-id="8c465-124">To configure the integration of Manabi Pocket into Azure AD, you need to add Manabi Pocket from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8c465-124">To configure the integration of Manabi Pocket into Azure AD, you need to add Manabi Pocket from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8c465-125">**To add Manabi Pocket from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8c465-125">**To add Manabi Pocket from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8c465-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8c465-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="8c465-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="8c465-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8c465-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8c465-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="8c465-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="8c465-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="8c465-133">In the search box, type **Manabi Pocket**, select **Manabi Pocket** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="8c465-133">In the search box, type **Manabi Pocket**, select **Manabi Pocket** from result panel then click **Add** button to add the application.</span></span>

    ![Manabi Pocket in the results list](./media/manabipocket-tutorial/tutorial_manabipocket_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8c465-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8c465-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8c465-136">In this section, you configure and test Azure AD single sign-on with Manabi Pocket based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8c465-136">In this section, you configure and test Azure AD single sign-on with Manabi Pocket based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8c465-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Manabi Pocket is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c465-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Manabi Pocket is to a user in Azure AD.</span></span> <span data-ttu-id="8c465-138">In other words, a link relationship between an Azure AD user and the related user in Manabi Pocket needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8c465-138">In other words, a link relationship between an Azure AD user and the related user in Manabi Pocket needs to be established.</span></span>

<span data-ttu-id="8c465-139">To configure and test Azure AD single sign-on with Manabi Pocket, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8c465-139">To configure and test Azure AD single sign-on with Manabi Pocket, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8c465-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8c465-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="8c465-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8c465-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="8c465-142">**[Create a Manabi Pocket test user](#create-a-manabi-pocket-test-user)** - to have a counterpart of Britta Simon in Manabi Pocket that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="8c465-142">**[Create a Manabi Pocket test user](#create-a-manabi-pocket-test-user)** - to have a counterpart of Britta Simon in Manabi Pocket that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="8c465-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8c465-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="8c465-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8c465-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8c465-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8c465-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8c465-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Manabi Pocket application.</span><span class="sxs-lookup"><span data-stu-id="8c465-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Manabi Pocket application.</span></span>

<span data-ttu-id="8c465-147">**To configure Azure AD single sign-on with Manabi Pocket, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8c465-147">**To configure Azure AD single sign-on with Manabi Pocket, perform the following steps:**</span></span>

1. <span data-ttu-id="8c465-148">In the Azure portal, on the **Manabi Pocket** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8c465-148">In the Azure portal, on the **Manabi Pocket** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="8c465-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8c465-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/manabipocket-tutorial/tutorial_manabipocket_samlbase.png)

1. <span data-ttu-id="8c465-152">On the **Manabi Pocket Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8c465-152">On the **Manabi Pocket Domain and URLs** section, perform the following steps:</span></span>

    ![Manabi Pocket Domain and URLs single sign-on information](./media/manabipocket-tutorial/tutorial_manabipocket_url.png)

    <span data-ttu-id="8c465-154">a.</span><span class="sxs-lookup"><span data-stu-id="8c465-154">a.</span></span> <span data-ttu-id="8c465-155">In the **Sign-on URL** textbox, type the URL: `https://ed-cl.com/`</span><span class="sxs-lookup"><span data-stu-id="8c465-155">In the **Sign-on URL** textbox, type the URL: `https://ed-cl.com/`</span></span>

    <span data-ttu-id="8c465-156">b.</span><span class="sxs-lookup"><span data-stu-id="8c465-156">b.</span></span> <span data-ttu-id="8c465-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<SERVER-NAME>.ed-cl.com/<TENANT-ID>/idp/provider`</span><span class="sxs-lookup"><span data-stu-id="8c465-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<SERVER-NAME>.ed-cl.com/<TENANT-ID>/idp/provider`</span></span>

    > [!NOTE]
    > <span data-ttu-id="8c465-158">The Identifier value is not real.</span><span class="sxs-lookup"><span data-stu-id="8c465-158">The Identifier value is not real.</span></span> <span data-ttu-id="8c465-159">Update this value with the actual Identifier .</span><span class="sxs-lookup"><span data-stu-id="8c465-159">Update this value with the actual Identifier .</span></span> <span data-ttu-id="8c465-160">Contact [Manabi Pocket Client support team](mailto:info-ed-cl@ntt.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="8c465-160">Contact [Manabi Pocket Client support team](mailto:info-ed-cl@ntt.com) to get this value.</span></span>

1. <span data-ttu-id="8c465-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8c465-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/manabipocket-tutorial/tutorial_manabipocket_certificate.png) 

1. <span data-ttu-id="8c465-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="8c465-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/manabipocket-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="8c465-165">To configure single sign-on on **Manabi Pocket** side, you need to send the downloaded **Metadata XML** to [Manabi Pocket support team](mailto:info-ed-cl@ntt.com).</span><span class="sxs-lookup"><span data-stu-id="8c465-165">To configure single sign-on on **Manabi Pocket** side, you need to send the downloaded **Metadata XML** to [Manabi Pocket support team](mailto:info-ed-cl@ntt.com).</span></span> <span data-ttu-id="8c465-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="8c465-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8c465-167">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8c465-167">Create an Azure AD test user</span></span>

<span data-ttu-id="8c465-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8c465-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="8c465-170">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8c465-170">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8c465-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="8c465-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/manabipocket-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="8c465-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="8c465-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/manabipocket-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="8c465-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="8c465-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/manabipocket-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="8c465-177">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8c465-177">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/manabipocket-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8c465-179">a.</span><span class="sxs-lookup"><span data-stu-id="8c465-179">a.</span></span> <span data-ttu-id="8c465-180">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8c465-180">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8c465-181">b.</span><span class="sxs-lookup"><span data-stu-id="8c465-181">b.</span></span> <span data-ttu-id="8c465-182">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8c465-182">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="8c465-183">c.</span><span class="sxs-lookup"><span data-stu-id="8c465-183">c.</span></span> <span data-ttu-id="8c465-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="8c465-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="8c465-185">d.</span><span class="sxs-lookup"><span data-stu-id="8c465-185">d.</span></span> <span data-ttu-id="8c465-186">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8c465-186">Click **Create**.</span></span>
 
### <a name="create-a-manabi-pocket-test-user"></a><span data-ttu-id="8c465-187">Create a Manabi Pocket test user</span><span class="sxs-lookup"><span data-stu-id="8c465-187">Create a Manabi Pocket test user</span></span>

<span data-ttu-id="8c465-188">In this section, you create a user called Britta Simon in Manabi Pocket.</span><span class="sxs-lookup"><span data-stu-id="8c465-188">In this section, you create a user called Britta Simon in Manabi Pocket.</span></span> <span data-ttu-id="8c465-189">Work with [Manabi Pocket support team](mailto:info-ed-cl@ntt.com) to add the users in the Manabi Pocket platform.</span><span class="sxs-lookup"><span data-stu-id="8c465-189">Work with [Manabi Pocket support team](mailto:info-ed-cl@ntt.com) to add the users in the Manabi Pocket platform.</span></span> <span data-ttu-id="8c465-190">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8c465-190">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8c465-191">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8c465-191">Assign the Azure AD test user</span></span>

<span data-ttu-id="8c465-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Manabi Pocket.</span><span class="sxs-lookup"><span data-stu-id="8c465-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Manabi Pocket.</span></span>

![Assign the user role][200] 

<span data-ttu-id="8c465-194">**To assign Britta Simon to Manabi Pocket, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8c465-194">**To assign Britta Simon to Manabi Pocket, perform the following steps:**</span></span>

1. <span data-ttu-id="8c465-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8c465-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="8c465-197">In the applications list, select **Manabi Pocket**.</span><span class="sxs-lookup"><span data-stu-id="8c465-197">In the applications list, select **Manabi Pocket**.</span></span>

    ![The Manabi Pocket link in the Applications list](./media/manabipocket-tutorial/tutorial_manabipocket_app.png)  

1. <span data-ttu-id="8c465-199">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="8c465-199">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="8c465-201">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="8c465-201">Click **Add** button.</span></span> <span data-ttu-id="8c465-202">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8c465-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="8c465-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="8c465-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="8c465-205">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="8c465-205">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="8c465-206">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8c465-206">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="8c465-207">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="8c465-207">Test single sign-on</span></span>

<span data-ttu-id="8c465-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8c465-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8c465-209">When you click the Manabi Pocket tile in the Access Panel, you should get automatically signed-on to your Manabi Pocket application.</span><span class="sxs-lookup"><span data-stu-id="8c465-209">When you click the Manabi Pocket tile in the Access Panel, you should get automatically signed-on to your Manabi Pocket application.</span></span>
<span data-ttu-id="8c465-210">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8c465-210">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8c465-211">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8c465-211">Additional resources</span></span>

* [<span data-ttu-id="8c465-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c465-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="8c465-213">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8c465-213">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/manabipocket-tutorial/tutorial_general_01.png
[2]: ./media/manabipocket-tutorial/tutorial_general_02.png
[3]: ./media/manabipocket-tutorial/tutorial_general_03.png
[4]: ./media/manabipocket-tutorial/tutorial_general_04.png

[100]: ./media/manabipocket-tutorial/tutorial_general_100.png

[200]: ./media/manabipocket-tutorial/tutorial_general_200.png
[201]: ./media/manabipocket-tutorial/tutorial_general_201.png
[202]: ./media/manabipocket-tutorial/tutorial_general_202.png
[203]: ./media/manabipocket-tutorial/tutorial_general_203.png