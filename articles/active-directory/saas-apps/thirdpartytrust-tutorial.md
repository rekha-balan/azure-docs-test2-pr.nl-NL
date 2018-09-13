---
title: 'Tutorial: Azure Active Directory integration with ThirdPartyTrust | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ThirdPartyTrust.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3c496939-4201-4108-b0cc-d3e7c4244229
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2018
ms.author: jeedes
ms.openlocfilehash: 4333f6094a0da22f73255836379e1163aac485d4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965924"
---
# <a name="tutorial-azure-active-directory-integration-with-thirdpartytrust"></a><span data-ttu-id="8cb39-103">Tutorial: Azure Active Directory integration with ThirdPartyTrust</span><span class="sxs-lookup"><span data-stu-id="8cb39-103">Tutorial: Azure Active Directory integration with ThirdPartyTrust</span></span>

<span data-ttu-id="8cb39-104">In this tutorial, you learn how to integrate ThirdPartyTrust with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8cb39-104">In this tutorial, you learn how to integrate ThirdPartyTrust with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8cb39-105">Integrating ThirdPartyTrust with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8cb39-105">Integrating ThirdPartyTrust with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8cb39-106">You can control in Azure AD who has access to ThirdPartyTrust.</span><span class="sxs-lookup"><span data-stu-id="8cb39-106">You can control in Azure AD who has access to ThirdPartyTrust.</span></span>
- <span data-ttu-id="8cb39-107">You can enable your users to automatically get signed-on to ThirdPartyTrust (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="8cb39-107">You can enable your users to automatically get signed-on to ThirdPartyTrust (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8cb39-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8cb39-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="8cb39-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="8cb39-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8cb39-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8cb39-110">Prerequisites</span></span>

<span data-ttu-id="8cb39-111">To configure Azure AD integration with ThirdPartyTrust, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8cb39-111">To configure Azure AD integration with ThirdPartyTrust, you need the following items:</span></span>

- <span data-ttu-id="8cb39-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8cb39-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8cb39-113">A ThirdPartyTrust single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8cb39-113">A ThirdPartyTrust single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8cb39-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8cb39-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8cb39-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8cb39-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8cb39-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="8cb39-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8cb39-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8cb39-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8cb39-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="8cb39-118">Scenario description</span></span>
<span data-ttu-id="8cb39-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8cb39-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8cb39-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8cb39-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8cb39-121">Adding ThirdPartyTrust from the gallery</span><span class="sxs-lookup"><span data-stu-id="8cb39-121">Adding ThirdPartyTrust from the gallery</span></span>
2. <span data-ttu-id="8cb39-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8cb39-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thirdpartytrust-from-the-gallery"></a><span data-ttu-id="8cb39-123">Adding ThirdPartyTrust from the gallery</span><span class="sxs-lookup"><span data-stu-id="8cb39-123">Adding ThirdPartyTrust from the gallery</span></span>
<span data-ttu-id="8cb39-124">To configure the integration of ThirdPartyTrust into Azure AD, you need to add ThirdPartyTrust from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8cb39-124">To configure the integration of ThirdPartyTrust into Azure AD, you need to add ThirdPartyTrust from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8cb39-125">**To add ThirdPartyTrust from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8cb39-125">**To add ThirdPartyTrust from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8cb39-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8cb39-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="8cb39-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="8cb39-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8cb39-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8cb39-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
3. <span data-ttu-id="8cb39-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="8cb39-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="8cb39-133">In the search box, type **ThirdPartyTrust**, select **ThirdPartyTrust** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="8cb39-133">In the search box, type **ThirdPartyTrust**, select **ThirdPartyTrust** from result panel then click **Add** button to add the application.</span></span>

    ![ThirdPartyTrust in the results list](./media/thirdpartytrust-tutorial/tutorial_thirdpartytrust_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8cb39-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8cb39-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8cb39-136">In this section, you configure and test Azure AD single sign-on with ThirdPartyTrust based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8cb39-136">In this section, you configure and test Azure AD single sign-on with ThirdPartyTrust based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8cb39-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ThirdPartyTrust is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cb39-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ThirdPartyTrust is to a user in Azure AD.</span></span> <span data-ttu-id="8cb39-138">In other words, a link relationship between an Azure AD user and the related user in ThirdPartyTrust needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8cb39-138">In other words, a link relationship between an Azure AD user and the related user in ThirdPartyTrust needs to be established.</span></span>

<span data-ttu-id="8cb39-139">To configure and test Azure AD single sign-on with ThirdPartyTrust, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8cb39-139">To configure and test Azure AD single sign-on with ThirdPartyTrust, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8cb39-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8cb39-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8cb39-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8cb39-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8cb39-142">**[Create a ThirdPartyTrust test user](#create-a-thirdpartytrust-test-user)** - to have a counterpart of Britta Simon in ThirdPartyTrust that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="8cb39-142">**[Create a ThirdPartyTrust test user](#create-a-thirdpartytrust-test-user)** - to have a counterpart of Britta Simon in ThirdPartyTrust that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8cb39-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8cb39-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8cb39-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8cb39-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8cb39-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8cb39-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8cb39-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ThirdPartyTrust application.</span><span class="sxs-lookup"><span data-stu-id="8cb39-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ThirdPartyTrust application.</span></span>

<span data-ttu-id="8cb39-147">**To configure Azure AD single sign-on with ThirdPartyTrust, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8cb39-147">**To configure Azure AD single sign-on with ThirdPartyTrust, perform the following steps:**</span></span>

1. <span data-ttu-id="8cb39-148">In the Azure portal, on the **ThirdPartyTrust** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8cb39-148">In the Azure portal, on the **ThirdPartyTrust** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="8cb39-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8cb39-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/thirdpartytrust-tutorial/tutorial_thirdpartytrust_samlbase.png)

3. <span data-ttu-id="8cb39-152">On the **ThirdPartyTrust Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="8cb39-152">On the **ThirdPartyTrust Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![ThirdPartyTrust Domain and URLs single sign-on information](./media/thirdpartytrust-tutorial/tutorial_thirdpartytrust_url.png)

    <span data-ttu-id="8cb39-154">In the **Identifier** textbox, type a URL: `https://api.thirdpartytrust.com/sai3/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="8cb39-154">In the **Identifier** textbox, type a URL: `https://api.thirdpartytrust.com/sai3/saml/metadata`</span></span>

4. <span data-ttu-id="8cb39-155">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="8cb39-155">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![ThirdPartyTrust Domain and URLs single sign-on information](./media/thirdpartytrust-tutorial/tutorial_thirdpartytrust_url1.png)

    <span data-ttu-id="8cb39-157">In the **Sign-on URL** textbox, type a URL: `https://api.thirdpartytrust.com/sai3/test`</span><span class="sxs-lookup"><span data-stu-id="8cb39-157">In the **Sign-on URL** textbox, type a URL: `https://api.thirdpartytrust.com/sai3/test`</span></span>
     
5. <span data-ttu-id="8cb39-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8cb39-158">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/thirdpartytrust-tutorial/tutorial_thirdpartytrust_certificate.png) 

6. <span data-ttu-id="8cb39-160">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="8cb39-160">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/thirdpartytrust-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="8cb39-162">To configure single sign-on on **ThirdPartyTrust** side, you need to send the downloaded **Metadata XML** to [ThirdPartyTrust support team](mailto:support@thirdpartytrust.com).</span><span class="sxs-lookup"><span data-stu-id="8cb39-162">To configure single sign-on on **ThirdPartyTrust** side, you need to send the downloaded **Metadata XML** to [ThirdPartyTrust support team](mailto:support@thirdpartytrust.com).</span></span> <span data-ttu-id="8cb39-163">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="8cb39-163">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8cb39-164">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="8cb39-164">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8cb39-165">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="8cb39-165">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8cb39-166">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8cb39-166">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8cb39-167">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8cb39-167">Create an Azure AD test user</span></span>

<span data-ttu-id="8cb39-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8cb39-168">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="8cb39-170">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8cb39-170">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8cb39-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="8cb39-171">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/thirdpartytrust-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="8cb39-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="8cb39-173">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/thirdpartytrust-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="8cb39-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="8cb39-175">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/thirdpartytrust-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="8cb39-177">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8cb39-177">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/thirdpartytrust-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8cb39-179">a.</span><span class="sxs-lookup"><span data-stu-id="8cb39-179">a.</span></span> <span data-ttu-id="8cb39-180">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8cb39-180">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8cb39-181">b.</span><span class="sxs-lookup"><span data-stu-id="8cb39-181">b.</span></span> <span data-ttu-id="8cb39-182">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8cb39-182">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="8cb39-183">c.</span><span class="sxs-lookup"><span data-stu-id="8cb39-183">c.</span></span> <span data-ttu-id="8cb39-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="8cb39-184">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="8cb39-185">d.</span><span class="sxs-lookup"><span data-stu-id="8cb39-185">d.</span></span> <span data-ttu-id="8cb39-186">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8cb39-186">Click **Create**.</span></span>
 
### <a name="create-a-thirdpartytrust-test-user"></a><span data-ttu-id="8cb39-187">Create a ThirdPartyTrust test user</span><span class="sxs-lookup"><span data-stu-id="8cb39-187">Create a ThirdPartyTrust test user</span></span>

<span data-ttu-id="8cb39-188">In this section, you create a user called Britta Simon in ThirdPartyTrust.</span><span class="sxs-lookup"><span data-stu-id="8cb39-188">In this section, you create a user called Britta Simon in ThirdPartyTrust.</span></span> <span data-ttu-id="8cb39-189">Work with [ThirdPartyTrust support team](mailto:support@thirdpartytrust.com) to add the users in the ThirdPartyTrust platform.</span><span class="sxs-lookup"><span data-stu-id="8cb39-189">Work with [ThirdPartyTrust support team](mailto:support@thirdpartytrust.com) to add the users in the ThirdPartyTrust platform.</span></span> <span data-ttu-id="8cb39-190">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8cb39-190">Users must be created and activated before you use single sign-on.</span></span> 


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8cb39-191">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8cb39-191">Assign the Azure AD test user</span></span>

<span data-ttu-id="8cb39-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ThirdPartyTrust.</span><span class="sxs-lookup"><span data-stu-id="8cb39-192">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ThirdPartyTrust.</span></span>

![Assign the user role][200] 

<span data-ttu-id="8cb39-194">**To assign Britta Simon to ThirdPartyTrust, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8cb39-194">**To assign Britta Simon to ThirdPartyTrust, perform the following steps:**</span></span>

1. <span data-ttu-id="8cb39-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8cb39-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="8cb39-197">In the applications list, select **ThirdPartyTrust**.</span><span class="sxs-lookup"><span data-stu-id="8cb39-197">In the applications list, select **ThirdPartyTrust**.</span></span>

    ![The ThirdPartyTrust link in the Applications list](./media/thirdpartytrust-tutorial/tutorial_thirdpartytrust_app.png)  

3. <span data-ttu-id="8cb39-199">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="8cb39-199">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="8cb39-201">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="8cb39-201">Click **Add** button.</span></span> <span data-ttu-id="8cb39-202">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8cb39-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="8cb39-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="8cb39-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8cb39-205">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="8cb39-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8cb39-206">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8cb39-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8cb39-207">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="8cb39-207">Test single sign-on</span></span>

<span data-ttu-id="8cb39-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8cb39-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8cb39-209">When you click the ThirdPartyTrust tile in the Access Panel, you should get automatically signed-on to your ThirdPartyTrust application.</span><span class="sxs-lookup"><span data-stu-id="8cb39-209">When you click the ThirdPartyTrust tile in the Access Panel, you should get automatically signed-on to your ThirdPartyTrust application.</span></span>
<span data-ttu-id="8cb39-210">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8cb39-210">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8cb39-211">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8cb39-211">Additional resources</span></span>

* [<span data-ttu-id="8cb39-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8cb39-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="8cb39-213">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8cb39-213">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/thirdpartytrust-tutorial/tutorial_general_01.png
[2]: ./media/thirdpartytrust-tutorial/tutorial_general_02.png
[3]: ./media/thirdpartytrust-tutorial/tutorial_general_03.png
[4]: ./media/thirdpartytrust-tutorial/tutorial_general_04.png

[100]: ./media/thirdpartytrust-tutorial/tutorial_general_100.png

[200]: ./media/thirdpartytrust-tutorial/tutorial_general_200.png
[201]: ./media/thirdpartytrust-tutorial/tutorial_general_201.png
[202]: ./media/thirdpartytrust-tutorial/tutorial_general_202.png
[203]: ./media/thirdpartytrust-tutorial/tutorial_general_203.png

