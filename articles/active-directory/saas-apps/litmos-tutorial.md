---
title: 'Tutorial: Azure Active Directory integration with Litmos | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Litmos.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: jeedes
ms.assetid: cfaae4bb-e8e5-41d1-ac88-8cc369653036
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: a0c70ee6419280b0975d77fb213f9406286708cc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866835"
---
# <a name="tutorial-azure-active-directory-integration-with-litmos"></a><span data-ttu-id="f5039-103">Tutorial: Azure Active Directory integration with Litmos</span><span class="sxs-lookup"><span data-stu-id="f5039-103">Tutorial: Azure Active Directory integration with Litmos</span></span>

<span data-ttu-id="f5039-104">In this tutorial, you learn how to integrate Litmos with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f5039-104">In this tutorial, you learn how to integrate Litmos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f5039-105">Integrating Litmos with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f5039-105">Integrating Litmos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f5039-106">You can control in Azure AD who has access to Litmos.</span><span class="sxs-lookup"><span data-stu-id="f5039-106">You can control in Azure AD who has access to Litmos.</span></span>
- <span data-ttu-id="f5039-107">You can enable your users to automatically get signed-on to Litmos (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="f5039-107">You can enable your users to automatically get signed-on to Litmos (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="f5039-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f5039-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="f5039-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="f5039-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5039-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f5039-110">Prerequisites</span></span>

<span data-ttu-id="f5039-111">To configure Azure AD integration with Litmos, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f5039-111">To configure Azure AD integration with Litmos, you need the following items:</span></span>

- <span data-ttu-id="f5039-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f5039-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f5039-113">A Litmos single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f5039-113">A Litmos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f5039-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="f5039-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f5039-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f5039-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f5039-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="f5039-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f5039-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f5039-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f5039-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="f5039-118">Scenario description</span></span>
<span data-ttu-id="f5039-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f5039-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f5039-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="f5039-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f5039-121">Adding Litmos from the gallery</span><span class="sxs-lookup"><span data-stu-id="f5039-121">Adding Litmos from the gallery</span></span>
1. <span data-ttu-id="f5039-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f5039-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-litmos-from-the-gallery"></a><span data-ttu-id="f5039-123">Adding Litmos from the gallery</span><span class="sxs-lookup"><span data-stu-id="f5039-123">Adding Litmos from the gallery</span></span>
<span data-ttu-id="f5039-124">To configure the integration of Litmos into Azure AD, you need to add Litmos from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f5039-124">To configure the integration of Litmos into Azure AD, you need to add Litmos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f5039-125">**To add Litmos from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f5039-125">**To add Litmos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f5039-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f5039-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="f5039-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="f5039-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f5039-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f5039-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="f5039-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="f5039-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="f5039-133">In the search box, type **Litmos**, select **Litmos** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="f5039-133">In the search box, type **Litmos**, select **Litmos** from result panel then click **Add** button to add the application.</span></span>

    ![Litmos in the results list](./media/litmos-tutorial/tutorial_litmos_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="f5039-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f5039-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="f5039-136">In this section, you configure and test Azure AD single sign-on with Litmos based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f5039-136">In this section, you configure and test Azure AD single sign-on with Litmos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f5039-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Litmos is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f5039-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Litmos is to a user in Azure AD.</span></span> <span data-ttu-id="f5039-138">In other words, a link relationship between an Azure AD user and the related user in Litmos needs to be established.</span><span class="sxs-lookup"><span data-stu-id="f5039-138">In other words, a link relationship between an Azure AD user and the related user in Litmos needs to be established.</span></span>

<span data-ttu-id="f5039-139">In Litmos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="f5039-139">In Litmos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f5039-140">To configure and test Azure AD single sign-on with Litmos, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f5039-140">To configure and test Azure AD single sign-on with Litmos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f5039-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f5039-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="f5039-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f5039-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="f5039-143">**[Create a Litmos test user](#create-a-litmos-test-user)** - to have a counterpart of Britta Simon in Litmos that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="f5039-143">**[Create a Litmos test user](#create-a-litmos-test-user)** - to have a counterpart of Britta Simon in Litmos that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="f5039-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f5039-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="f5039-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="f5039-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="f5039-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f5039-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="f5039-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Litmos application.</span><span class="sxs-lookup"><span data-stu-id="f5039-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Litmos application.</span></span>

<span data-ttu-id="f5039-148">**To configure Azure AD single sign-on with Litmos, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f5039-148">**To configure Azure AD single sign-on with Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="f5039-149">In the Azure portal, on the **Litmos** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f5039-149">In the Azure portal, on the **Litmos** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="f5039-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f5039-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/litmos-tutorial/tutorial_litmos_samlbase.png)

1. <span data-ttu-id="f5039-153">On the **Litmos Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f5039-153">On the **Litmos Domain and URLs** section, perform the following steps:</span></span>

    ![Litmos Domain and URLs single sign-on information](./media/litmos-tutorial/tutorial_litmos_url.png)

    <span data-ttu-id="f5039-155">a.</span><span class="sxs-lookup"><span data-stu-id="f5039-155">a.</span></span> <span data-ttu-id="f5039-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.litmos.com/account/Login`</span><span class="sxs-lookup"><span data-stu-id="f5039-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.litmos.com/account/Login`</span></span>

    <span data-ttu-id="f5039-157">b.</span><span class="sxs-lookup"><span data-stu-id="f5039-157">b.</span></span> <span data-ttu-id="f5039-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.litmos.com/integration/samllogin`</span><span class="sxs-lookup"><span data-stu-id="f5039-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.litmos.com/integration/samllogin`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f5039-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="f5039-159">These values are not real.</span></span> <span data-ttu-id="f5039-160">Update these values with the actual Identifier and Reply URL, which are explained later in tutorial or contact [Litmos support team](https://www.litmos.com/contact-us/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="f5039-160">Update these values with the actual Identifier and Reply URL, which are explained later in tutorial or contact [Litmos support team](https://www.litmos.com/contact-us/) to get these values.</span></span>

1. <span data-ttu-id="f5039-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="f5039-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/litmos-tutorial/tutorial_litmos_certificate.png)

1. <span data-ttu-id="f5039-163">As part of the configuration, you need to customize the **SAML Token Attributes** for your Litmos application.</span><span class="sxs-lookup"><span data-stu-id="f5039-163">As part of the configuration, you need to customize the **SAML Token Attributes** for your Litmos application.</span></span>

    ![Attribute Section](./media/litmos-tutorial/tutorial_attribute.png)
           
    | <span data-ttu-id="f5039-165">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="f5039-165">Attribute Name</span></span>   | <span data-ttu-id="f5039-166">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="f5039-166">Attribute Value</span></span> |   
    | ---------------  | ----------------|
    | <span data-ttu-id="f5039-167">FirstName</span><span class="sxs-lookup"><span data-stu-id="f5039-167">FirstName</span></span> |<span data-ttu-id="f5039-168">user.givenname</span><span class="sxs-lookup"><span data-stu-id="f5039-168">user.givenname</span></span> |
    | <span data-ttu-id="f5039-169">LastName</span><span class="sxs-lookup"><span data-stu-id="f5039-169">LastName</span></span>  |<span data-ttu-id="f5039-170">user.surname</span><span class="sxs-lookup"><span data-stu-id="f5039-170">user.surname</span></span> |
    | <span data-ttu-id="f5039-171">Email</span><span class="sxs-lookup"><span data-stu-id="f5039-171">Email</span></span> |<span data-ttu-id="f5039-172">user.mail</span><span class="sxs-lookup"><span data-stu-id="f5039-172">user.mail</span></span> |

    <span data-ttu-id="f5039-173">a.</span><span class="sxs-lookup"><span data-stu-id="f5039-173">a.</span></span> <span data-ttu-id="f5039-174">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="f5039-174">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Add attribute](./media/litmos-tutorial/tutorial_attribute_04.png)

    ![Add attribute Dailog](./media/litmos-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="f5039-177">b.</span><span class="sxs-lookup"><span data-stu-id="f5039-177">b.</span></span> <span data-ttu-id="f5039-178">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="f5039-178">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    <span data-ttu-id="f5039-179">c.</span><span class="sxs-lookup"><span data-stu-id="f5039-179">c.</span></span> <span data-ttu-id="f5039-180">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="f5039-180">From the **Value** list, type the attribute value shown for that row.</span></span>
    
    <span data-ttu-id="f5039-181">d.</span><span class="sxs-lookup"><span data-stu-id="f5039-181">d.</span></span> <span data-ttu-id="f5039-182">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="f5039-182">Click **Ok**.</span></span>     

1. <span data-ttu-id="f5039-183">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="f5039-183">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/litmos-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="f5039-185">In a different browser window, sign-on to your Litmos company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="f5039-185">In a different browser window, sign-on to your Litmos company site as administrator.</span></span>

1. <span data-ttu-id="f5039-186">In the navigation bar on the left side, click **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="f5039-186">In the navigation bar on the left side, click **Accounts**.</span></span>
   
    ![Accounts Section on App Side][22] 

1. <span data-ttu-id="f5039-188">Click the **Integrations** tab.</span><span class="sxs-lookup"><span data-stu-id="f5039-188">Click the **Integrations** tab.</span></span>
   
    ![Integration Tab][23] 

1. <span data-ttu-id="f5039-190">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span><span class="sxs-lookup"><span data-stu-id="f5039-190">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0 Section][24] 

1. <span data-ttu-id="f5039-192">Copy the value under **The SAML endpoint for litmos is:** and paste it into the **Reply URL** textbox in the **Litmos Domain and URLs** section in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f5039-192">Copy the value under **The SAML endpoint for litmos is:** and paste it into the **Reply URL** textbox in the **Litmos Domain and URLs** section in Azure portal.</span></span> 
   
    ![SAML endpoint][26] 

1. <span data-ttu-id="f5039-194">In your **Litmos** application, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f5039-194">In your **Litmos** application, perform the following steps:</span></span>
    
     ![Litmos Application][25] 
     
     <span data-ttu-id="f5039-196">a.</span><span class="sxs-lookup"><span data-stu-id="f5039-196">a.</span></span> <span data-ttu-id="f5039-197">Click **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="f5039-197">Click **Enable SAML**.</span></span>
    
     <span data-ttu-id="f5039-198">b.</span><span class="sxs-lookup"><span data-stu-id="f5039-198">b.</span></span> <span data-ttu-id="f5039-199">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **SAML X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="f5039-199">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **SAML X.509 Certificate** textbox.</span></span>
     
     <span data-ttu-id="f5039-200">c.</span><span class="sxs-lookup"><span data-stu-id="f5039-200">c.</span></span> <span data-ttu-id="f5039-201">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="f5039-201">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="f5039-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="f5039-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f5039-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="f5039-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f5039-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f5039-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="f5039-205">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f5039-205">Create an Azure AD test user</span></span>

<span data-ttu-id="f5039-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f5039-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="f5039-208">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f5039-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f5039-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="f5039-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/litmos-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="f5039-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="f5039-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/litmos-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="f5039-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="f5039-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/litmos-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="f5039-215">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f5039-215">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/litmos-tutorial/create_aaduser_04.png)

    <span data-ttu-id="f5039-217">a.</span><span class="sxs-lookup"><span data-stu-id="f5039-217">a.</span></span> <span data-ttu-id="f5039-218">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f5039-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f5039-219">b.</span><span class="sxs-lookup"><span data-stu-id="f5039-219">b.</span></span> <span data-ttu-id="f5039-220">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f5039-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="f5039-221">c.</span><span class="sxs-lookup"><span data-stu-id="f5039-221">c.</span></span> <span data-ttu-id="f5039-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="f5039-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="f5039-223">d.</span><span class="sxs-lookup"><span data-stu-id="f5039-223">d.</span></span> <span data-ttu-id="f5039-224">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f5039-224">Click **Create**.</span></span>
  
### <a name="create-a-litmos-test-user"></a><span data-ttu-id="f5039-225">Create a Litmos test user</span><span class="sxs-lookup"><span data-stu-id="f5039-225">Create a Litmos test user</span></span>

<span data-ttu-id="f5039-226">The objective of this section is to create a user called Britta Simon in Litmos.</span><span class="sxs-lookup"><span data-stu-id="f5039-226">The objective of this section is to create a user called Britta Simon in Litmos.</span></span>  
<span data-ttu-id="f5039-227">The Litmos application supports Just-in-Time provisioning.</span><span class="sxs-lookup"><span data-stu-id="f5039-227">The Litmos application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="f5039-228">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f5039-228">This means, a user account is automatically created if necessary during an attempt to access the application using the Access Panel.</span></span>

<span data-ttu-id="f5039-229">**To create a user called Britta Simon in Litmos, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f5039-229">**To create a user called Britta Simon in Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="f5039-230">In a different browser window, sign-on to your Litmos company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="f5039-230">In a different browser window, sign-on to your Litmos company site as administrator.</span></span>

1. <span data-ttu-id="f5039-231">In the navigation bar on the left side, click **Accounts**.</span><span class="sxs-lookup"><span data-stu-id="f5039-231">In the navigation bar on the left side, click **Accounts**.</span></span>
   
    ![Accounts Section On App Side][22] 

1. <span data-ttu-id="f5039-233">Click the **Integrations** tab.</span><span class="sxs-lookup"><span data-stu-id="f5039-233">Click the **Integrations** tab.</span></span>
   
    ![Integrations Tab][23] 

1. <span data-ttu-id="f5039-235">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span><span class="sxs-lookup"><span data-stu-id="f5039-235">On the **Integrations** tab, scroll down to **3rd Party Integrations**, and then click **SAML 2.0** tab.</span></span>
   
    ![SAML 2.0][24] 
    
1. <span data-ttu-id="f5039-237">Select **Autogenerate Users**</span><span class="sxs-lookup"><span data-stu-id="f5039-237">Select **Autogenerate Users**</span></span>
   
    ![Autogenerate Users][27] 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="f5039-239">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f5039-239">Assign the Azure AD test user</span></span>

<span data-ttu-id="f5039-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Litmos.</span><span class="sxs-lookup"><span data-stu-id="f5039-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Litmos.</span></span>

![Assign the user role][200] 

<span data-ttu-id="f5039-242">**To assign Britta Simon to Litmos, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f5039-242">**To assign Britta Simon to Litmos, perform the following steps:**</span></span>

1. <span data-ttu-id="f5039-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f5039-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="f5039-245">In the applications list, select **Litmos**.</span><span class="sxs-lookup"><span data-stu-id="f5039-245">In the applications list, select **Litmos**.</span></span>

    ![The Litmos link in the Applications list](./media/litmos-tutorial/tutorial_litmos_app.png)  

1. <span data-ttu-id="f5039-247">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="f5039-247">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="f5039-249">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="f5039-249">Click **Add** button.</span></span> <span data-ttu-id="f5039-250">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f5039-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="f5039-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="f5039-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="f5039-253">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="f5039-253">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="f5039-254">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f5039-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="f5039-255">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="f5039-255">Test single sign-on</span></span>

<span data-ttu-id="f5039-256">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f5039-256">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="f5039-257">When you click the Litmos tile in the Access Panel, you should get automatically signed-on to your Litmos application.</span><span class="sxs-lookup"><span data-stu-id="f5039-257">When you click the Litmos tile in the Access Panel, you should get automatically signed-on to your Litmos application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f5039-258">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f5039-258">Additional resources</span></span>

* [<span data-ttu-id="f5039-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f5039-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="f5039-260">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f5039-260">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/litmos-tutorial/tutorial_general_01.png
[2]: ./media/litmos-tutorial/tutorial_general_02.png
[3]: ./media/litmos-tutorial/tutorial_general_03.png
[4]: ./media/litmos-tutorial/tutorial_general_04.png
[21]: ./media/litmos-tutorial/tutorial_litmos_60.png
[22]: ./media/litmos-tutorial/tutorial_litmos_61.png
[23]: ./media/litmos-tutorial/tutorial_litmos_62.png
[24]: ./media/litmos-tutorial/tutorial_litmos_63.png
[25]: ./media/litmos-tutorial/tutorial_litmos_64.png
[26]: ./media/litmos-tutorial/tutorial_litmos_65.png
[27]: ./media/litmos-tutorial/tutorial_litmos_66.png

[100]: ./media/litmos-tutorial/tutorial_general_100.png

[200]: ./media/litmos-tutorial/tutorial_general_200.png
[201]: ./media/litmos-tutorial/tutorial_general_201.png
[202]: ./media/litmos-tutorial/tutorial_general_202.png
[203]: ./media/litmos-tutorial/tutorial_general_203.png

