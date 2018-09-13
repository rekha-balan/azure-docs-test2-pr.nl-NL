---
title: 'Tutorial: Azure Active Directory integration with Adobe Captivate Prime | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Adobe Captivate Prime.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2f95b226-1465-47f4-b8b7-de4b0772abbc
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2018
ms.author: jeedes
ms.openlocfilehash: bbeae2cadde3e64f17b20eafabaf5e2dbf5a5cc6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869414"
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-captivate-prime"></a><span data-ttu-id="de506-103">Tutorial: Azure Active Directory integration with Adobe Captivate Prime</span><span class="sxs-lookup"><span data-stu-id="de506-103">Tutorial: Azure Active Directory integration with Adobe Captivate Prime</span></span>

<span data-ttu-id="de506-104">In this tutorial, you learn how to integrate Adobe Captivate Prime with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="de506-104">In this tutorial, you learn how to integrate Adobe Captivate Prime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="de506-105">Integrating Adobe Captivate Prime with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="de506-105">Integrating Adobe Captivate Prime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="de506-106">You can control in Azure AD who has access to Adobe Captivate Prime.</span><span class="sxs-lookup"><span data-stu-id="de506-106">You can control in Azure AD who has access to Adobe Captivate Prime.</span></span>
- <span data-ttu-id="de506-107">You can enable your users to automatically get signed-on to Adobe Captivate Prime (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="de506-107">You can enable your users to automatically get signed-on to Adobe Captivate Prime (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="de506-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="de506-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="de506-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="de506-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de506-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="de506-110">Prerequisites</span></span>

<span data-ttu-id="de506-111">To configure Azure AD integration with Adobe Captivate Prime, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="de506-111">To configure Azure AD integration with Adobe Captivate Prime, you need the following items:</span></span>

- <span data-ttu-id="de506-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="de506-112">An Azure AD subscription</span></span>
- <span data-ttu-id="de506-113">An Adobe Captivate Prime single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="de506-113">An Adobe Captivate Prime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="de506-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="de506-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="de506-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="de506-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="de506-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="de506-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="de506-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="de506-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="de506-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="de506-118">Scenario description</span></span>
<span data-ttu-id="de506-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="de506-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="de506-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="de506-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="de506-121">Adding Adobe Captivate Prime from the gallery</span><span class="sxs-lookup"><span data-stu-id="de506-121">Adding Adobe Captivate Prime from the gallery</span></span>
2. <span data-ttu-id="de506-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="de506-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-captivate-prime-from-the-gallery"></a><span data-ttu-id="de506-123">Adding Adobe Captivate Prime from the gallery</span><span class="sxs-lookup"><span data-stu-id="de506-123">Adding Adobe Captivate Prime from the gallery</span></span>
<span data-ttu-id="de506-124">To configure the integration of Adobe Captivate Prime into Azure AD, you need to add Adobe Captivate Prime from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="de506-124">To configure the integration of Adobe Captivate Prime into Azure AD, you need to add Adobe Captivate Prime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="de506-125">**To add Adobe Captivate Prime from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="de506-125">**To add Adobe Captivate Prime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="de506-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="de506-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="de506-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="de506-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="de506-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="de506-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="de506-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="de506-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="de506-133">In the search box, type **Adobe Captivate Prime**, select **Adobe Captivate Prime** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="de506-133">In the search box, type **Adobe Captivate Prime**, select **Adobe Captivate Prime** from result panel then click **Add** button to add the application.</span></span>

    ![Adobe Captivate Prime in the results list](./media/adobecaptivateprime-tutorial/tutorial_adobecaptivateprime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="de506-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="de506-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="de506-136">In this section, you configure and test Azure AD single sign-on with Adobe Captivate Prime based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="de506-136">In this section, you configure and test Azure AD single sign-on with Adobe Captivate Prime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="de506-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Captivate Prime is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de506-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Adobe Captivate Prime is to a user in Azure AD.</span></span> <span data-ttu-id="de506-138">In other words, a link relationship between an Azure AD user and the related user in Adobe Captivate Prime needs to be established.</span><span class="sxs-lookup"><span data-stu-id="de506-138">In other words, a link relationship between an Azure AD user and the related user in Adobe Captivate Prime needs to be established.</span></span>

<span data-ttu-id="de506-139">To configure and test Azure AD single sign-on with Adobe Captivate Prime, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="de506-139">To configure and test Azure AD single sign-on with Adobe Captivate Prime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="de506-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="de506-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="de506-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="de506-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="de506-142">**[Create an Adobe Captivate Prime test user](#create-an-adobe-captivate-prime-test-user)** - to have a counterpart of Britta Simon in Adobe Captivate Prime that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="de506-142">**[Create an Adobe Captivate Prime test user](#create-an-adobe-captivate-prime-test-user)** - to have a counterpart of Britta Simon in Adobe Captivate Prime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="de506-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="de506-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="de506-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="de506-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="de506-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="de506-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="de506-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adobe Captivate Prime application.</span><span class="sxs-lookup"><span data-stu-id="de506-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Adobe Captivate Prime application.</span></span>

<span data-ttu-id="de506-147">**To configure Azure AD single sign-on with Adobe Captivate Prime, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="de506-147">**To configure Azure AD single sign-on with Adobe Captivate Prime, perform the following steps:**</span></span>

1. <span data-ttu-id="de506-148">In the Azure portal, on the **Adobe Captivate Prime** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="de506-148">In the Azure portal, on the **Adobe Captivate Prime** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="de506-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="de506-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/adobecaptivateprime-tutorial/tutorial_adobecaptivateprime_samlbase.png)

3. <span data-ttu-id="de506-152">On the **Adobe Captivate Prime Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="de506-152">On the **Adobe Captivate Prime Domain and URLs** section, perform the following steps:</span></span>

    ![Adobe Captivate Prime Domain and URLs single sign-on information](./media/adobecaptivateprime-tutorial/tutorial_adobecaptivateprime_url.png)

    <span data-ttu-id="de506-154">a.</span><span class="sxs-lookup"><span data-stu-id="de506-154">a.</span></span> <span data-ttu-id="de506-155">In the **Identifier** textbox, type a URL: `https://captivateprime.adobe.com`</span><span class="sxs-lookup"><span data-stu-id="de506-155">In the **Identifier** textbox, type a URL: `https://captivateprime.adobe.com`</span></span>

    <span data-ttu-id="de506-156">b.</span><span class="sxs-lookup"><span data-stu-id="de506-156">b.</span></span> <span data-ttu-id="de506-157">In the **Reply URL** textbox, type a URL: `https://captivateprime.adobe.com/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="de506-157">In the **Reply URL** textbox, type a URL: `https://captivateprime.adobe.com/saml/SSO`</span></span>

4. <span data-ttu-id="de506-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="de506-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/adobecaptivateprime-tutorial/tutorial_adobecaptivateprime_certificate.png) 

5. <span data-ttu-id="de506-160">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="de506-160">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/adobecaptivateprime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="de506-162">Go to **Properties** tab, copy the **User access URL** and paste it in Notepad.</span><span class="sxs-lookup"><span data-stu-id="de506-162">Go to **Properties** tab, copy the **User access URL** and paste it in Notepad.</span></span>

    ![The user access link](./media/adobecaptivateprime-tutorial/tutorial_adobecaptivateprime_appprop.png)

7. <span data-ttu-id="de506-164">To configure single sign-on on **Adobe Captivate Prime** side, you need to send the downloaded **Metadata XML** and copied **User access URL** to [Adobe Captivate Prime support team](mailto:captivateprimesupport@adobe.com).</span><span class="sxs-lookup"><span data-stu-id="de506-164">To configure single sign-on on **Adobe Captivate Prime** side, you need to send the downloaded **Metadata XML** and copied **User access URL** to [Adobe Captivate Prime support team](mailto:captivateprimesupport@adobe.com).</span></span> <span data-ttu-id="de506-165">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="de506-165">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="de506-166">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="de506-166">Create an Azure AD test user</span></span>

<span data-ttu-id="de506-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="de506-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="de506-169">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="de506-169">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="de506-170">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="de506-170">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/adobecaptivateprime-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="de506-172">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="de506-172">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/adobecaptivateprime-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="de506-174">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="de506-174">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/adobecaptivateprime-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="de506-176">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="de506-176">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/adobecaptivateprime-tutorial/create_aaduser_04.png)

    <span data-ttu-id="de506-178">a.</span><span class="sxs-lookup"><span data-stu-id="de506-178">a.</span></span> <span data-ttu-id="de506-179">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="de506-179">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="de506-180">b.</span><span class="sxs-lookup"><span data-stu-id="de506-180">b.</span></span> <span data-ttu-id="de506-181">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="de506-181">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="de506-182">c.</span><span class="sxs-lookup"><span data-stu-id="de506-182">c.</span></span> <span data-ttu-id="de506-183">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="de506-183">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="de506-184">d.</span><span class="sxs-lookup"><span data-stu-id="de506-184">d.</span></span> <span data-ttu-id="de506-185">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="de506-185">Click **Create**.</span></span>
  
### <a name="create-an-adobe-captivate-prime-test-user"></a><span data-ttu-id="de506-186">Create an Adobe Captivate Prime test user</span><span class="sxs-lookup"><span data-stu-id="de506-186">Create an Adobe Captivate Prime test user</span></span>

<span data-ttu-id="de506-187">In this section, you create a user called Britta Simon in Adobe Captivate Prime.</span><span class="sxs-lookup"><span data-stu-id="de506-187">In this section, you create a user called Britta Simon in Adobe Captivate Prime.</span></span> <span data-ttu-id="de506-188">Work with [Adobe Captivate Prime support team](mailto:captivateprimesupport@adobe.com) to add the users in the Adobe Captivate Prime platform.</span><span class="sxs-lookup"><span data-stu-id="de506-188">Work with [Adobe Captivate Prime support team](mailto:captivateprimesupport@adobe.com) to add the users in the Adobe Captivate Prime platform.</span></span> <span data-ttu-id="de506-189">Users must be created and activated before you use single sign-on</span><span class="sxs-lookup"><span data-stu-id="de506-189">Users must be created and activated before you use single sign-on</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="de506-190">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="de506-190">Assign the Azure AD test user</span></span>

<span data-ttu-id="de506-191">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adobe Captivate Prime.</span><span class="sxs-lookup"><span data-stu-id="de506-191">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Adobe Captivate Prime.</span></span>

![Assign the user role][200] 

<span data-ttu-id="de506-193">**To assign Britta Simon to Adobe Captivate Prime, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="de506-193">**To assign Britta Simon to Adobe Captivate Prime, perform the following steps:**</span></span>

1. <span data-ttu-id="de506-194">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="de506-194">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="de506-196">In the applications list, select **Adobe Captivate Prime**.</span><span class="sxs-lookup"><span data-stu-id="de506-196">In the applications list, select **Adobe Captivate Prime**.</span></span>

    ![The Adobe Captivate Prime link in the Applications list](./media/adobecaptivateprime-tutorial/tutorial_adobecaptivateprime_app.png)  

3. <span data-ttu-id="de506-198">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="de506-198">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="de506-200">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="de506-200">Click **Add** button.</span></span> <span data-ttu-id="de506-201">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="de506-201">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="de506-203">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="de506-203">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="de506-204">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="de506-204">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="de506-205">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="de506-205">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="de506-206">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="de506-206">Test single sign-on</span></span>

<span data-ttu-id="de506-207">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="de506-207">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="de506-208">When you click the Adobe Captivate Prime tile in the Access Panel, you should get automatically signed-on to your Adobe Captivate Prime application.</span><span class="sxs-lookup"><span data-stu-id="de506-208">When you click the Adobe Captivate Prime tile in the Access Panel, you should get automatically signed-on to your Adobe Captivate Prime application.</span></span>
<span data-ttu-id="de506-209">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="de506-209">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="de506-210">Additional resources</span><span class="sxs-lookup"><span data-stu-id="de506-210">Additional resources</span></span>

* [<span data-ttu-id="de506-211">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="de506-211">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="de506-212">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="de506-212">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/adobecaptivateprime-tutorial/tutorial_general_01.png
[2]: ./media/adobecaptivateprime-tutorial/tutorial_general_02.png
[3]: ./media/adobecaptivateprime-tutorial/tutorial_general_03.png
[4]: ./media/adobecaptivateprime-tutorial/tutorial_general_04.png

[100]: ./media/adobecaptivateprime-tutorial/tutorial_general_100.png

[200]: ./media/adobecaptivateprime-tutorial/tutorial_general_200.png
[201]: ./media/adobecaptivateprime-tutorial/tutorial_general_201.png
[202]: ./media/adobecaptivateprime-tutorial/tutorial_general_202.png
[203]: ./media/adobecaptivateprime-tutorial/tutorial_general_203.png

