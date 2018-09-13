---
title: 'Tutorial: Azure Active Directory integration with Reflektive | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Reflektive.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 799a08b9-1ce6-46d1-9064-aa9f36f6604e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/24/2017
ms.author: jeedes
ms.openlocfilehash: 228bcc2e43337876b211158f70fe1136de494c85
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866959"
---
# <a name="tutorial-azure-active-directory-integration-with-reflektive"></a><span data-ttu-id="65aa5-103">Tutorial: Azure Active Directory integration with Reflektive</span><span class="sxs-lookup"><span data-stu-id="65aa5-103">Tutorial: Azure Active Directory integration with Reflektive</span></span>

<span data-ttu-id="65aa5-104">In this tutorial, you learn how to integrate Reflektive with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="65aa5-104">In this tutorial, you learn how to integrate Reflektive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="65aa5-105">Integrating Reflektive with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="65aa5-105">Integrating Reflektive with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="65aa5-106">You can control in Azure AD who has access to Reflektive.</span><span class="sxs-lookup"><span data-stu-id="65aa5-106">You can control in Azure AD who has access to Reflektive.</span></span>
- <span data-ttu-id="65aa5-107">You can enable your users to automatically get signed-on to Reflektive (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="65aa5-107">You can enable your users to automatically get signed-on to Reflektive (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="65aa5-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="65aa5-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="65aa5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="65aa5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65aa5-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="65aa5-110">Prerequisites</span></span>

<span data-ttu-id="65aa5-111">To configure Azure AD integration with Reflektive, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="65aa5-111">To configure Azure AD integration with Reflektive, you need the following items:</span></span>

- <span data-ttu-id="65aa5-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="65aa5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="65aa5-113">A Reflektive single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="65aa5-113">A Reflektive single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="65aa5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="65aa5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="65aa5-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="65aa5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="65aa5-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="65aa5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="65aa5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="65aa5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="65aa5-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="65aa5-118">Scenario description</span></span>
<span data-ttu-id="65aa5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="65aa5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="65aa5-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="65aa5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="65aa5-121">Adding Reflektive from the gallery</span><span class="sxs-lookup"><span data-stu-id="65aa5-121">Adding Reflektive from the gallery</span></span>
2. <span data-ttu-id="65aa5-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="65aa5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-reflektive-from-the-gallery"></a><span data-ttu-id="65aa5-123">Adding Reflektive from the gallery</span><span class="sxs-lookup"><span data-stu-id="65aa5-123">Adding Reflektive from the gallery</span></span>
<span data-ttu-id="65aa5-124">To configure the integration of Reflektive into Azure AD, you need to add Reflektive from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="65aa5-124">To configure the integration of Reflektive into Azure AD, you need to add Reflektive from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="65aa5-125">**To add Reflektive from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="65aa5-125">**To add Reflektive from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="65aa5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="65aa5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="65aa5-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="65aa5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="65aa5-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="65aa5-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="65aa5-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="65aa5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="65aa5-133">In the search box, type **Reflektive**, select **Reflektive** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="65aa5-133">In the search box, type **Reflektive**, select **Reflektive** from result panel then click **Add** button to add the application.</span></span>

    ![Reflektive in the results list](./media/reflektive-tutorial/tutorial_reflektive_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="65aa5-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="65aa5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="65aa5-136">In this section, you configure and test Azure AD single sign-on with Reflektive based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="65aa5-136">In this section, you configure and test Azure AD single sign-on with Reflektive based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="65aa5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Reflektive is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="65aa5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Reflektive is to a user in Azure AD.</span></span> <span data-ttu-id="65aa5-138">In other words, a link relationship between an Azure AD user and the related user in Reflektive needs to be established.</span><span class="sxs-lookup"><span data-stu-id="65aa5-138">In other words, a link relationship between an Azure AD user and the related user in Reflektive needs to be established.</span></span>

<span data-ttu-id="65aa5-139">In Reflektive, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="65aa5-139">In Reflektive, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="65aa5-140">To configure and test Azure AD single sign-on with Reflektive, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="65aa5-140">To configure and test Azure AD single sign-on with Reflektive, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="65aa5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="65aa5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="65aa5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="65aa5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="65aa5-143">**[Create a Reflektive test user](#create-a-reflektive-test-user)** - to have a counterpart of Britta Simon in Reflektive that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="65aa5-143">**[Create a Reflektive test user](#create-a-reflektive-test-user)** - to have a counterpart of Britta Simon in Reflektive that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="65aa5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="65aa5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="65aa5-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="65aa5-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="65aa5-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="65aa5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="65aa5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Reflektive application.</span><span class="sxs-lookup"><span data-stu-id="65aa5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Reflektive application.</span></span>

<span data-ttu-id="65aa5-148">**To configure Azure AD single sign-on with Reflektive, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="65aa5-148">**To configure Azure AD single sign-on with Reflektive, perform the following steps:**</span></span>

1. <span data-ttu-id="65aa5-149">In the Azure portal, on the **Reflektive** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="65aa5-149">In the Azure portal, on the **Reflektive** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="65aa5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="65aa5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/reflektive-tutorial/tutorial_reflektive_samlbase.png)

3. <span data-ttu-id="65aa5-153">On the **Reflektive Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span><span class="sxs-lookup"><span data-stu-id="65aa5-153">On the **Reflektive Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Reflektive Domain and URLs single sign-on information](./media/reflektive-tutorial/tutorial_reflektive_url.png)

    <span data-ttu-id="65aa5-155">In the **Identifier** textbox, use one of the below URL as per confirmation from the reflective support team:</span><span class="sxs-lookup"><span data-stu-id="65aa5-155">In the **Identifier** textbox, use one of the below URL as per confirmation from the reflective support team:</span></span>
    | |
    |--|
    | `reflektive.com` |
    | `https://www.reflektive.com/saml/metadata` |

4. <span data-ttu-id="65aa5-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="65aa5-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Reflektive Domain and URLs single sign-on information](./media/reflektive-tutorial/tutorial_reflektive_url1.png)

    <span data-ttu-id="65aa5-158">In the **Sign-on URL** textbox, type a URL: `https://www.reflektive.com/app`</span><span class="sxs-lookup"><span data-stu-id="65aa5-158">In the **Sign-on URL** textbox, type a URL: `https://www.reflektive.com/app`</span></span>

    > [!NOTE]
    > <span data-ttu-id="65aa5-159">For SP mode you need to get the email id registered with [Reflektive support team](https://support@reflektive.com).</span><span class="sxs-lookup"><span data-stu-id="65aa5-159">For SP mode you need to get the email id registered with [Reflektive support team](https://support@reflektive.com).</span></span> <span data-ttu-id="65aa5-160">When you enter your ID in the **Email** textbox then the single sign-on option will be enabled.</span><span class="sxs-lookup"><span data-stu-id="65aa5-160">When you enter your ID in the **Email** textbox then the single sign-on option will be enabled.</span></span>
         
5. <span data-ttu-id="65aa5-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="65aa5-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/reflektive-tutorial/tutorial_reflektive_certificate.png) 

6. <span data-ttu-id="65aa5-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="65aa5-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/reflektive-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="65aa5-165">To configure single sign-on on **Reflektive** side, you need to send the downloaded **Metadata XML** to [Reflektive support team](https://support@reflektive.com).</span><span class="sxs-lookup"><span data-stu-id="65aa5-165">To configure single sign-on on **Reflektive** side, you need to send the downloaded **Metadata XML** to [Reflektive support team](https://support@reflektive.com).</span></span> <span data-ttu-id="65aa5-166">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="65aa5-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="65aa5-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="65aa5-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="65aa5-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="65aa5-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="65aa5-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="65aa5-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="65aa5-170">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="65aa5-170">Create an Azure AD test user</span></span>

<span data-ttu-id="65aa5-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="65aa5-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="65aa5-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="65aa5-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="65aa5-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="65aa5-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/reflektive-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="65aa5-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="65aa5-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/reflektive-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="65aa5-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="65aa5-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/reflektive-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="65aa5-180">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="65aa5-180">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/reflektive-tutorial/create_aaduser_04.png)

    <span data-ttu-id="65aa5-182">a.</span><span class="sxs-lookup"><span data-stu-id="65aa5-182">a.</span></span> <span data-ttu-id="65aa5-183">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="65aa5-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="65aa5-184">b.</span><span class="sxs-lookup"><span data-stu-id="65aa5-184">b.</span></span> <span data-ttu-id="65aa5-185">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="65aa5-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="65aa5-186">c.</span><span class="sxs-lookup"><span data-stu-id="65aa5-186">c.</span></span> <span data-ttu-id="65aa5-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="65aa5-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="65aa5-188">d.</span><span class="sxs-lookup"><span data-stu-id="65aa5-188">d.</span></span> <span data-ttu-id="65aa5-189">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="65aa5-189">Click **Create**.</span></span>
 
### <a name="create-a-reflektive-test-user"></a><span data-ttu-id="65aa5-190">Create a Reflektive test user</span><span class="sxs-lookup"><span data-stu-id="65aa5-190">Create a Reflektive test user</span></span>

<span data-ttu-id="65aa5-191">In this section, you create a user called Britta Simon in Reflektive.</span><span class="sxs-lookup"><span data-stu-id="65aa5-191">In this section, you create a user called Britta Simon in Reflektive.</span></span> <span data-ttu-id="65aa5-192">Work with [Reflektive support team](mailto:support@reflektive.com) to add the users in the Reflektive platform.</span><span class="sxs-lookup"><span data-stu-id="65aa5-192">Work with [Reflektive support team](mailto:support@reflektive.com) to add the users in the Reflektive platform.</span></span> <span data-ttu-id="65aa5-193">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="65aa5-193">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="65aa5-194">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="65aa5-194">Assign the Azure AD test user</span></span>

<span data-ttu-id="65aa5-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Reflektive.</span><span class="sxs-lookup"><span data-stu-id="65aa5-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Reflektive.</span></span>

![Assign the user role][200] 

<span data-ttu-id="65aa5-197">**To assign Britta Simon to Reflektive, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="65aa5-197">**To assign Britta Simon to Reflektive, perform the following steps:**</span></span>

1. <span data-ttu-id="65aa5-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="65aa5-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="65aa5-200">In the applications list, select **Reflektive**.</span><span class="sxs-lookup"><span data-stu-id="65aa5-200">In the applications list, select **Reflektive**.</span></span>

    ![The Reflektive link in the Applications list](./media/reflektive-tutorial/tutorial_reflektive_app.png)  

3. <span data-ttu-id="65aa5-202">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="65aa5-202">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="65aa5-204">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="65aa5-204">Click **Add** button.</span></span> <span data-ttu-id="65aa5-205">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="65aa5-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="65aa5-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="65aa5-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="65aa5-208">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="65aa5-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="65aa5-209">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="65aa5-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="65aa5-210">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="65aa5-210">Test single sign-on</span></span>

<span data-ttu-id="65aa5-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="65aa5-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="65aa5-212">When you click the Reflektive tile in the Access Panel, you should get automatically signed-on to your Reflektive application.</span><span class="sxs-lookup"><span data-stu-id="65aa5-212">When you click the Reflektive tile in the Access Panel, you should get automatically signed-on to your Reflektive application.</span></span>
<span data-ttu-id="65aa5-213">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="65aa5-213">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="65aa5-214">Additional resources</span><span class="sxs-lookup"><span data-stu-id="65aa5-214">Additional resources</span></span>

* [<span data-ttu-id="65aa5-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65aa5-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="65aa5-216">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="65aa5-216">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/reflektive-tutorial/tutorial_general_01.png
[2]: ./media/reflektive-tutorial/tutorial_general_02.png
[3]: ./media/reflektive-tutorial/tutorial_general_03.png
[4]: ./media/reflektive-tutorial/tutorial_general_04.png

[100]: ./media/reflektive-tutorial/tutorial_general_100.png

[200]: ./media/reflektive-tutorial/tutorial_general_200.png
[201]: ./media/reflektive-tutorial/tutorial_general_201.png
[202]: ./media/reflektive-tutorial/tutorial_general_202.png
[203]: ./media/reflektive-tutorial/tutorial_general_203.png

