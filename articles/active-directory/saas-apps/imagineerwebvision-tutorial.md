---
title: 'Tutorial: Azure Active Directory integration with Imagineer WebVision | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Imagineer WebVision.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b936a3f4-74c1-4437-b0f7-6d1b1de38bb1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2018
ms.author: jeedes
ms.openlocfilehash: d86004680bf13c9716b4ff4e7a41af73ea186f27
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864625"
---
# <a name="tutorial-azure-active-directory-integration-with-imagineer-webvision"></a><span data-ttu-id="6e014-103">Tutorial: Azure Active Directory integration with Imagineer WebVision</span><span class="sxs-lookup"><span data-stu-id="6e014-103">Tutorial: Azure Active Directory integration with Imagineer WebVision</span></span>

<span data-ttu-id="6e014-104">In this tutorial, you learn how to integrate Imagineer WebVision with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6e014-104">In this tutorial, you learn how to integrate Imagineer WebVision with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6e014-105">Integrating Imagineer WebVision with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="6e014-105">Integrating Imagineer WebVision with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6e014-106">You can control in Azure AD who has access to Imagineer WebVision.</span><span class="sxs-lookup"><span data-stu-id="6e014-106">You can control in Azure AD who has access to Imagineer WebVision.</span></span>
- <span data-ttu-id="6e014-107">You can enable your users to automatically get signed-on to Imagineer WebVision (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="6e014-107">You can enable your users to automatically get signed-on to Imagineer WebVision (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6e014-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6e014-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="6e014-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="6e014-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e014-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6e014-110">Prerequisites</span></span>

<span data-ttu-id="6e014-111">To configure Azure AD integration with Imagineer WebVision, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="6e014-111">To configure Azure AD integration with Imagineer WebVision, you need the following items:</span></span>

- <span data-ttu-id="6e014-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="6e014-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6e014-113">An Imagineer WebVision single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="6e014-113">An Imagineer WebVision single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6e014-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="6e014-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6e014-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="6e014-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6e014-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="6e014-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6e014-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6e014-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6e014-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="6e014-118">Scenario description</span></span>
<span data-ttu-id="6e014-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="6e014-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6e014-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="6e014-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6e014-121">Adding Imagineer WebVision from the gallery</span><span class="sxs-lookup"><span data-stu-id="6e014-121">Adding Imagineer WebVision from the gallery</span></span>
2. <span data-ttu-id="6e014-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6e014-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-imagineer-webvision-from-the-gallery"></a><span data-ttu-id="6e014-123">Adding Imagineer WebVision from the gallery</span><span class="sxs-lookup"><span data-stu-id="6e014-123">Adding Imagineer WebVision from the gallery</span></span>
<span data-ttu-id="6e014-124">To configure the integration of Imagineer WebVision into Azure AD, you need to add Imagineer WebVision from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="6e014-124">To configure the integration of Imagineer WebVision into Azure AD, you need to add Imagineer WebVision from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6e014-125">**To add Imagineer WebVision from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6e014-125">**To add Imagineer WebVision from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6e014-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="6e014-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="6e014-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="6e014-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6e014-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6e014-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="6e014-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="6e014-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="6e014-133">In the search box, type **Imagineer WebVision**, select **Imagineer WebVision** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="6e014-133">In the search box, type **Imagineer WebVision**, select **Imagineer WebVision** from result panel then click **Add** button to add the application.</span></span>

    ![Imagineer WebVision in the results list](./media/imagineerwebvision-tutorial/tutorial_imagineerwebvision_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6e014-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6e014-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6e014-136">In this section, you configure and test Azure AD single sign-on with Imagineer WebVision based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6e014-136">In this section, you configure and test Azure AD single sign-on with Imagineer WebVision based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6e014-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Imagineer WebVision is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6e014-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Imagineer WebVision is to a user in Azure AD.</span></span> <span data-ttu-id="6e014-138">In other words, a link relationship between an Azure AD user and the related user in Imagineer WebVision needs to be established.</span><span class="sxs-lookup"><span data-stu-id="6e014-138">In other words, a link relationship between an Azure AD user and the related user in Imagineer WebVision needs to be established.</span></span>

<span data-ttu-id="6e014-139">To configure and test Azure AD single sign-on with Imagineer WebVision, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="6e014-139">To configure and test Azure AD single sign-on with Imagineer WebVision, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6e014-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="6e014-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6e014-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6e014-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6e014-142">**[Create an Imagineer WebVision test user](#create-an-imagineer-webvision-test-user)** - to have a counterpart of Britta Simon in Imagineer WebVision that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="6e014-142">**[Create an Imagineer WebVision test user](#create-an-imagineer-webvision-test-user)** - to have a counterpart of Britta Simon in Imagineer WebVision that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6e014-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6e014-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6e014-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="6e014-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6e014-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6e014-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6e014-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Imagineer WebVision application.</span><span class="sxs-lookup"><span data-stu-id="6e014-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Imagineer WebVision application.</span></span>

<span data-ttu-id="6e014-147">**To configure Azure AD single sign-on with Imagineer WebVision, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6e014-147">**To configure Azure AD single sign-on with Imagineer WebVision, perform the following steps:**</span></span>

1. <span data-ttu-id="6e014-148">In the Azure portal, on the **Imagineer WebVision** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6e014-148">In the Azure portal, on the **Imagineer WebVision** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="6e014-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6e014-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/imagineerwebvision-tutorial/tutorial_imagineerwebvision_samlbase.png)

3. <span data-ttu-id="6e014-152">On the **Imagineer WebVision Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6e014-152">On the **Imagineer WebVision Domain and URLs** section, perform the following steps:</span></span>

    ![Imagineer WebVision Domain and URLs single sign-on information](./media/imagineerwebvision-tutorial/tutorial_imagineerwebvision_url.png)

    <span data-ttu-id="6e014-154">a.</span><span class="sxs-lookup"><span data-stu-id="6e014-154">a.</span></span> <span data-ttu-id="6e014-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<YOUR SERVER URL>/<yourapplicationloginpage>`</span><span class="sxs-lookup"><span data-stu-id="6e014-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<YOUR SERVER URL>/<yourapplicationloginpage>`</span></span>

    <span data-ttu-id="6e014-156">b.</span><span class="sxs-lookup"><span data-stu-id="6e014-156">b.</span></span> <span data-ttu-id="6e014-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<YOUR SERVER URL>/<yourapplicationloginpage>`</span><span class="sxs-lookup"><span data-stu-id="6e014-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<YOUR SERVER URL>/<yourapplicationloginpage>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6e014-158">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="6e014-158">These values are not real.</span></span> <span data-ttu-id="6e014-159">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="6e014-159">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6e014-160">Contact [Imagineer WebVision Client support team](mailto:support@itgny.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="6e014-160">Contact [Imagineer WebVision Client support team](mailto:support@itgny.com) to get these values.</span></span>

4. <span data-ttu-id="6e014-161">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span><span class="sxs-lookup"><span data-stu-id="6e014-161">On the **SAML Signing Certificate** section, click the copy button to copy **App Federation Metadata Url** and paste it into notepad.</span></span>

    ![The Certificate download link](./media/imagineerwebvision-tutorial/tutorial_imagineerwebvision_certificate.png) 

5. <span data-ttu-id="6e014-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="6e014-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/imagineerwebvision-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6e014-165">To configure single sign-on on **Imagineer WebVision** side, you need to send the copied **App Federation Metadata Url** to [Imagineer WebVision support team](mailto:support@itgny.com).</span><span class="sxs-lookup"><span data-stu-id="6e014-165">To configure single sign-on on **Imagineer WebVision** side, you need to send the copied **App Federation Metadata Url** to [Imagineer WebVision support team](mailto:support@itgny.com).</span></span> <span data-ttu-id="6e014-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="6e014-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6e014-167">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6e014-167">Create an Azure AD test user</span></span>

<span data-ttu-id="6e014-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6e014-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="6e014-170">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6e014-170">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6e014-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="6e014-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/imagineerwebvision-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6e014-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="6e014-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/imagineerwebvision-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6e014-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="6e014-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/imagineerwebvision-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6e014-177">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6e014-177">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/imagineerwebvision-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6e014-179">a.</span><span class="sxs-lookup"><span data-stu-id="6e014-179">a.</span></span> <span data-ttu-id="6e014-180">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6e014-180">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6e014-181">b.</span><span class="sxs-lookup"><span data-stu-id="6e014-181">b.</span></span> <span data-ttu-id="6e014-182">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6e014-182">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="6e014-183">c.</span><span class="sxs-lookup"><span data-stu-id="6e014-183">c.</span></span> <span data-ttu-id="6e014-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="6e014-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="6e014-185">d.</span><span class="sxs-lookup"><span data-stu-id="6e014-185">d.</span></span> <span data-ttu-id="6e014-186">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6e014-186">Click **Create**.</span></span>
 
### <a name="create-an-imagineer-webvision-test-user"></a><span data-ttu-id="6e014-187">Create an Imagineer WebVision test user</span><span class="sxs-lookup"><span data-stu-id="6e014-187">Create an Imagineer WebVision test user</span></span>

<span data-ttu-id="6e014-188">In this section, you create a user called Britta Simon in Imagineer WebVision.</span><span class="sxs-lookup"><span data-stu-id="6e014-188">In this section, you create a user called Britta Simon in Imagineer WebVision.</span></span> <span data-ttu-id="6e014-189">Work with [Imagineer WebVision support team](mailto:support@itgny.com) to add the users in the Imagineer WebVision platform.</span><span class="sxs-lookup"><span data-stu-id="6e014-189">Work with [Imagineer WebVision support team](mailto:support@itgny.com) to add the users in the Imagineer WebVision platform.</span></span> <span data-ttu-id="6e014-190">Users must be created and activated before you use single sign-on</span><span class="sxs-lookup"><span data-stu-id="6e014-190">Users must be created and activated before you use single sign-on</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6e014-191">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6e014-191">Assign the Azure AD test user</span></span>

<span data-ttu-id="6e014-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Imagineer WebVision.</span><span class="sxs-lookup"><span data-stu-id="6e014-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Imagineer WebVision.</span></span>

![Assign the user role][200] 

<span data-ttu-id="6e014-194">**To assign Britta Simon to Imagineer WebVision, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6e014-194">**To assign Britta Simon to Imagineer WebVision, perform the following steps:**</span></span>

1. <span data-ttu-id="6e014-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6e014-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="6e014-197">In the applications list, select **Imagineer WebVision**.</span><span class="sxs-lookup"><span data-stu-id="6e014-197">In the applications list, select **Imagineer WebVision**.</span></span>

    ![The Imagineer WebVision link in the Applications list](./media/imagineerwebvision-tutorial/tutorial_imagineerwebvision_app.png)  

3. <span data-ttu-id="6e014-199">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="6e014-199">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="6e014-201">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="6e014-201">Click **Add** button.</span></span> <span data-ttu-id="6e014-202">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6e014-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="6e014-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="6e014-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6e014-205">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="6e014-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6e014-206">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6e014-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6e014-207">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="6e014-207">Test single sign-on</span></span>

<span data-ttu-id="6e014-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="6e014-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6e014-209">When you click the Imagineer WebVision tile in the Access Panel, you should get automatically signed-on to your Imagineer WebVision application.</span><span class="sxs-lookup"><span data-stu-id="6e014-209">When you click the Imagineer WebVision tile in the Access Panel, you should get automatically signed-on to your Imagineer WebVision application.</span></span>
<span data-ttu-id="6e014-210">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6e014-210">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6e014-211">Additional resources</span><span class="sxs-lookup"><span data-stu-id="6e014-211">Additional resources</span></span>

* [<span data-ttu-id="6e014-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6e014-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="6e014-213">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6e014-213">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/imagineerwebvision-tutorial/tutorial_general_01.png
[2]: ./media/imagineerwebvision-tutorial/tutorial_general_02.png
[3]: ./media/imagineerwebvision-tutorial/tutorial_general_03.png
[4]: ./media/imagineerwebvision-tutorial/tutorial_general_04.png

[100]: ./media/imagineerwebvision-tutorial/tutorial_general_100.png

[200]: ./media/imagineerwebvision-tutorial/tutorial_general_200.png
[201]: ./media/imagineerwebvision-tutorial/tutorial_general_201.png
[202]: ./media/imagineerwebvision-tutorial/tutorial_general_202.png
[203]: ./media/imagineerwebvision-tutorial/tutorial_general_203.png

