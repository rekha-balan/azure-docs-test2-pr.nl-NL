---
title: 'Tutorial: Azure Active Directory integration with Carlson Wagonlit Travel | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Carlson Wagonlit Travel.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2745e165-94ab-43b1-970a-4547b4e5b501
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2018
ms.author: jeedes
ms.openlocfilehash: b1854b8e2c05fb2bcc5bd864c9ed8049250743b8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868458"
---
# <a name="tutorial-azure-active-directory-integration-with-carlson-wagonlit-travel"></a><span data-ttu-id="240d2-103">Tutorial: Azure Active Directory integration with Carlson Wagonlit Travel</span><span class="sxs-lookup"><span data-stu-id="240d2-103">Tutorial: Azure Active Directory integration with Carlson Wagonlit Travel</span></span>

<span data-ttu-id="240d2-104">In this tutorial, you learn how to integrate Carlson Wagonlit Travel with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="240d2-104">In this tutorial, you learn how to integrate Carlson Wagonlit Travel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="240d2-105">Integrating Carlson Wagonlit Travel with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="240d2-105">Integrating Carlson Wagonlit Travel with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="240d2-106">You can control in Azure AD who has access to Carlson Wagonlit Travel.</span><span class="sxs-lookup"><span data-stu-id="240d2-106">You can control in Azure AD who has access to Carlson Wagonlit Travel.</span></span>
- <span data-ttu-id="240d2-107">You can enable your users to automatically get signed-on to Carlson Wagonlit Travel (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="240d2-107">You can enable your users to automatically get signed-on to Carlson Wagonlit Travel (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="240d2-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="240d2-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="240d2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="240d2-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="240d2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="240d2-110">Prerequisites</span></span>

<span data-ttu-id="240d2-111">To configure Azure AD integration with Carlson Wagonlit Travel, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="240d2-111">To configure Azure AD integration with Carlson Wagonlit Travel, you need the following items:</span></span>

- <span data-ttu-id="240d2-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="240d2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="240d2-113">A Carlson Wagonlit Travel single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="240d2-113">A Carlson Wagonlit Travel single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="240d2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="240d2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="240d2-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="240d2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="240d2-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="240d2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="240d2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="240d2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="240d2-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="240d2-118">Scenario description</span></span>
<span data-ttu-id="240d2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="240d2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="240d2-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="240d2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="240d2-121">Adding Carlson Wagonlit Travel from the gallery</span><span class="sxs-lookup"><span data-stu-id="240d2-121">Adding Carlson Wagonlit Travel from the gallery</span></span>
2. <span data-ttu-id="240d2-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="240d2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-carlson-wagonlit-travel-from-the-gallery"></a><span data-ttu-id="240d2-123">Adding Carlson Wagonlit Travel from the gallery</span><span class="sxs-lookup"><span data-stu-id="240d2-123">Adding Carlson Wagonlit Travel from the gallery</span></span>
<span data-ttu-id="240d2-124">To configure the integration of Carlson Wagonlit Travel into Azure AD, you need to add Carlson Wagonlit Travel from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="240d2-124">To configure the integration of Carlson Wagonlit Travel into Azure AD, you need to add Carlson Wagonlit Travel from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="240d2-125">**To add Carlson Wagonlit Travel from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="240d2-125">**To add Carlson Wagonlit Travel from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="240d2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="240d2-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="240d2-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="240d2-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="240d2-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="240d2-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="240d2-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="240d2-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="240d2-133">In the search box, type **Carlson Wagonlit Travel**, select **Carlson Wagonlit Travel** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="240d2-133">In the search box, type **Carlson Wagonlit Travel**, select **Carlson Wagonlit Travel** from result panel then click **Add** button to add the application.</span></span>

    ![Carlson Wagonlit Travel in the results list](./media/carlsonwagonlit-tutorial/tutorial_carlsonwagonlittravel_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="240d2-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="240d2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="240d2-136">In this section, you configure and test Azure AD single sign-on with Carlson Wagonlit Travel based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="240d2-136">In this section, you configure and test Azure AD single sign-on with Carlson Wagonlit Travel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="240d2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Carlson Wagonlit Travel is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="240d2-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Carlson Wagonlit Travel is to a user in Azure AD.</span></span> <span data-ttu-id="240d2-138">In other words, a link relationship between an Azure AD user and the related user in Carlson Wagonlit Travel needs to be established.</span><span class="sxs-lookup"><span data-stu-id="240d2-138">In other words, a link relationship between an Azure AD user and the related user in Carlson Wagonlit Travel needs to be established.</span></span>

<span data-ttu-id="240d2-139">In Carlson Wagonlit Travel, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="240d2-139">In Carlson Wagonlit Travel, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="240d2-140">To configure and test Azure AD single sign-on with Carlson Wagonlit Travel, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="240d2-140">To configure and test Azure AD single sign-on with Carlson Wagonlit Travel, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="240d2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="240d2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="240d2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="240d2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="240d2-143">**[Create a Carlson Wagonlit Travel test user](#create-a-carlson-wagonlit-travel-test-user)** - to have a counterpart of Britta Simon in Carlson Wagonlit Travel that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="240d2-143">**[Create a Carlson Wagonlit Travel test user](#create-a-carlson-wagonlit-travel-test-user)** - to have a counterpart of Britta Simon in Carlson Wagonlit Travel that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="240d2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="240d2-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="240d2-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="240d2-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="240d2-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="240d2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="240d2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Carlson Wagonlit Travel application.</span><span class="sxs-lookup"><span data-stu-id="240d2-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Carlson Wagonlit Travel application.</span></span>

<span data-ttu-id="240d2-148">**To configure Azure AD single sign-on with Carlson Wagonlit Travel, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="240d2-148">**To configure Azure AD single sign-on with Carlson Wagonlit Travel, perform the following steps:**</span></span>

1. <span data-ttu-id="240d2-149">In the Azure portal, on the **Carlson Wagonlit Travel** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="240d2-149">In the Azure portal, on the **Carlson Wagonlit Travel** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="240d2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="240d2-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/carlsonwagonlit-tutorial/tutorial_carlsonwagonlittravel_samlbase.png)

3. <span data-ttu-id="240d2-153">On the **Carlson Wagonlit Travel Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="240d2-153">On the **Carlson Wagonlit Travel Domain and URLs** section, perform the following steps:</span></span>

    ![Carlson Wagonlit Travel Domain and URLs single sign-on information](./media/carlsonwagonlit-tutorial/tutorial_carlsonwagonlittravel_url.png)

    <span data-ttu-id="240d2-155">In the **Identifier** textbox, type the value: `cwt-stage`</span><span class="sxs-lookup"><span data-stu-id="240d2-155">In the **Identifier** textbox, type the value: `cwt-stage`</span></span>

4. <span data-ttu-id="240d2-156">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="240d2-156">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/carlsonwagonlit-tutorial/tutorial_carlsonwagonlittravel_certificate.png) 

5. <span data-ttu-id="240d2-158">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="240d2-158">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/carlsonwagonlit-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="240d2-160">To configure single sign-on on **Carlson Wagonlit Travel** side, you need to send the downloaded **Metadata XML** to [Carlson Wagonlit Travel support team](http://www.carlsonwagonlit.in/content/cwt/in/en/technical-assistance.html).</span><span class="sxs-lookup"><span data-stu-id="240d2-160">To configure single sign-on on **Carlson Wagonlit Travel** side, you need to send the downloaded **Metadata XML** to [Carlson Wagonlit Travel support team](http://www.carlsonwagonlit.in/content/cwt/in/en/technical-assistance.html).</span></span> <span data-ttu-id="240d2-161">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="240d2-161">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="240d2-162">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="240d2-162">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="240d2-163">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="240d2-163">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="240d2-164">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="240d2-164">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="240d2-165">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="240d2-165">Create an Azure AD test user</span></span>

<span data-ttu-id="240d2-166">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="240d2-166">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="240d2-168">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="240d2-168">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="240d2-169">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="240d2-169">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/carlsonwagonlit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="240d2-171">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="240d2-171">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/carlsonwagonlit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="240d2-173">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="240d2-173">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/carlsonwagonlit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="240d2-175">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="240d2-175">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/carlsonwagonlit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="240d2-177">a.</span><span class="sxs-lookup"><span data-stu-id="240d2-177">a.</span></span> <span data-ttu-id="240d2-178">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="240d2-178">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="240d2-179">b.</span><span class="sxs-lookup"><span data-stu-id="240d2-179">b.</span></span> <span data-ttu-id="240d2-180">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="240d2-180">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="240d2-181">c.</span><span class="sxs-lookup"><span data-stu-id="240d2-181">c.</span></span> <span data-ttu-id="240d2-182">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="240d2-182">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="240d2-183">d.</span><span class="sxs-lookup"><span data-stu-id="240d2-183">d.</span></span> <span data-ttu-id="240d2-184">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="240d2-184">Click **Create**.</span></span>
 
### <a name="create-a-carlson-wagonlit-travel-test-user"></a><span data-ttu-id="240d2-185">Create a Carlson Wagonlit Travel test user</span><span class="sxs-lookup"><span data-stu-id="240d2-185">Create a Carlson Wagonlit Travel test user</span></span>

<span data-ttu-id="240d2-186">In this section, you create a user called Britta Simon in Carlson Wagonlit Travel.</span><span class="sxs-lookup"><span data-stu-id="240d2-186">In this section, you create a user called Britta Simon in Carlson Wagonlit Travel.</span></span> <span data-ttu-id="240d2-187">Work with [Carlson Wagonlit Travel support team](http://www.carlsonwagonlit.in/content/cwt/in/en/technical-assistance.html) to add the users in the Carlson Wagonlit Travel platform.</span><span class="sxs-lookup"><span data-stu-id="240d2-187">Work with [Carlson Wagonlit Travel support team](http://www.carlsonwagonlit.in/content/cwt/in/en/technical-assistance.html) to add the users in the Carlson Wagonlit Travel platform.</span></span> <span data-ttu-id="240d2-188">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="240d2-188">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="240d2-189">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="240d2-189">Assign the Azure AD test user</span></span>

<span data-ttu-id="240d2-190">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Carlson Wagonlit Travel.</span><span class="sxs-lookup"><span data-stu-id="240d2-190">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Carlson Wagonlit Travel.</span></span>

![Assign the user role][200] 

<span data-ttu-id="240d2-192">**To assign Britta Simon to Carlson Wagonlit Travel, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="240d2-192">**To assign Britta Simon to Carlson Wagonlit Travel, perform the following steps:**</span></span>

1. <span data-ttu-id="240d2-193">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="240d2-193">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="240d2-195">In the applications list, select **Carlson Wagonlit Travel**.</span><span class="sxs-lookup"><span data-stu-id="240d2-195">In the applications list, select **Carlson Wagonlit Travel**.</span></span>

    ![The Carlson Wagonlit Travel link in the Applications list](./media/carlsonwagonlit-tutorial/tutorial_carlsonwagonlittravel_app.png)  

3. <span data-ttu-id="240d2-197">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="240d2-197">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="240d2-199">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="240d2-199">Click **Add** button.</span></span> <span data-ttu-id="240d2-200">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="240d2-200">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="240d2-202">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="240d2-202">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="240d2-203">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="240d2-203">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="240d2-204">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="240d2-204">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="240d2-205">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="240d2-205">Test single sign-on</span></span>

<span data-ttu-id="240d2-206">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="240d2-206">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="240d2-207">When you click the Carlson Wagonlit Travel tile in the Access Panel, you should get automatically signed-on to your Carlson Wagonlit Travel application.</span><span class="sxs-lookup"><span data-stu-id="240d2-207">When you click the Carlson Wagonlit Travel tile in the Access Panel, you should get automatically signed-on to your Carlson Wagonlit Travel application.</span></span>
<span data-ttu-id="240d2-208">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="240d2-208">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="240d2-209">Additional resources</span><span class="sxs-lookup"><span data-stu-id="240d2-209">Additional resources</span></span>

* [<span data-ttu-id="240d2-210">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="240d2-210">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="240d2-211">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="240d2-211">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/carlsonwagonlittravel-tutorial/tutorial_general_01.png
[2]: ./media/carlsonwagonlittravel-tutorial/tutorial_general_02.png
[3]: ./media/carlsonwagonlittravel-tutorial/tutorial_general_03.png
[4]: ./media/carlsonwagonlittravel-tutorial/tutorial_general_04.png

[100]: ./media/carlsonwagonlittravel-tutorial/tutorial_general_100.png

[200]: ./media/carlsonwagonlittravel-tutorial/tutorial_general_200.png
[201]: ./media/carlsonwagonlittravel-tutorial/tutorial_general_201.png
[202]: ./media/carlsonwagonlittravel-tutorial/tutorial_general_202.png
[203]: ./media/carlsonwagonlittravel-tutorial/tutorial_general_203.png

