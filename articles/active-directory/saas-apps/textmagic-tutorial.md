---
title: 'Tutorial: Azure Active Directory integration with TextMagic | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and TextMagic.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 3e5b49d2-7096-46bc-a9ce-90e09177ba28
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/16/2017
ms.author: jeedes
ms.openlocfilehash: b8ffd732221604d55c65d4623de89f716bba49eb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866191"
---
# <a name="tutorial-azure-active-directory-integration-with-textmagic"></a><span data-ttu-id="6c8ef-103">Tutorial: Azure Active Directory integration with TextMagic</span><span class="sxs-lookup"><span data-stu-id="6c8ef-103">Tutorial: Azure Active Directory integration with TextMagic</span></span>

<span data-ttu-id="6c8ef-104">In this tutorial, you learn how to integrate TextMagic with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6c8ef-104">In this tutorial, you learn how to integrate TextMagic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6c8ef-105">Integrating TextMagic with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="6c8ef-105">Integrating TextMagic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6c8ef-106">You can control in Azure AD who has access to TextMagic.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-106">You can control in Azure AD who has access to TextMagic.</span></span>
- <span data-ttu-id="6c8ef-107">You can enable your users to automatically get signed-on to TextMagic (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-107">You can enable your users to automatically get signed-on to TextMagic (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6c8ef-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="6c8ef-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="6c8ef-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c8ef-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6c8ef-110">Prerequisites</span></span>

<span data-ttu-id="6c8ef-111">To configure Azure AD integration with TextMagic, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="6c8ef-111">To configure Azure AD integration with TextMagic, you need the following items:</span></span>

- <span data-ttu-id="6c8ef-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="6c8ef-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6c8ef-113">A TextMagic single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="6c8ef-113">A TextMagic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6c8ef-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6c8ef-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="6c8ef-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6c8ef-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6c8ef-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6c8ef-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6c8ef-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="6c8ef-118">Scenario description</span></span>
<span data-ttu-id="6c8ef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6c8ef-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="6c8ef-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6c8ef-121">Adding TextMagic from the gallery</span><span class="sxs-lookup"><span data-stu-id="6c8ef-121">Adding TextMagic from the gallery</span></span>
1. <span data-ttu-id="6c8ef-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6c8ef-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-textmagic-from-the-gallery"></a><span data-ttu-id="6c8ef-123">Adding TextMagic from the gallery</span><span class="sxs-lookup"><span data-stu-id="6c8ef-123">Adding TextMagic from the gallery</span></span>
<span data-ttu-id="6c8ef-124">To configure the integration of TextMagic into Azure AD, you need to add TextMagic from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-124">To configure the integration of TextMagic into Azure AD, you need to add TextMagic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6c8ef-125">**To add TextMagic from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6c8ef-125">**To add TextMagic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6c8ef-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="6c8ef-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6c8ef-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="6c8ef-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="6c8ef-133">In the search box, type **TextMagic**, select **TextMagic** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-133">In the search box, type **TextMagic**, select **TextMagic** from result panel then click **Add** button to add the application.</span></span>

    ![TextMagic in the results list](./media/textmagic-tutorial/tutorial_textmagic_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6c8ef-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6c8ef-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6c8ef-136">In this section, you configure and test Azure AD single sign-on with TextMagic based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="6c8ef-136">In this section, you configure and test Azure AD single sign-on with TextMagic based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6c8ef-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TextMagic is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TextMagic is to a user in Azure AD.</span></span> <span data-ttu-id="6c8ef-138">In other words, a link relationship between an Azure AD user and the related user in TextMagic needs to be established.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-138">In other words, a link relationship between an Azure AD user and the related user in TextMagic needs to be established.</span></span>

<span data-ttu-id="6c8ef-139">In TextMagic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-139">In TextMagic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6c8ef-140">To configure and test Azure AD single sign-on with TextMagic, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="6c8ef-140">To configure and test Azure AD single sign-on with TextMagic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6c8ef-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="6c8ef-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="6c8ef-143">**[Create a TextMagic test user](#create-a-textmagic-test-user)** - to have a counterpart of Britta Simon in TextMagic that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-143">**[Create a TextMagic test user](#create-a-textmagic-test-user)** - to have a counterpart of Britta Simon in TextMagic that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="6c8ef-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="6c8ef-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6c8ef-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6c8ef-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6c8ef-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TextMagic application.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TextMagic application.</span></span>

<span data-ttu-id="6c8ef-148">**To configure Azure AD single sign-on with TextMagic, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6c8ef-148">**To configure Azure AD single sign-on with TextMagic, perform the following steps:**</span></span>

1. <span data-ttu-id="6c8ef-149">In the Azure portal, on the **TextMagic** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-149">In the Azure portal, on the **TextMagic** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="6c8ef-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/textmagic-tutorial/tutorial_textmagic_samlbase.png)

1. <span data-ttu-id="6c8ef-153">On the **TextMagic Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="6c8ef-153">On the **TextMagic Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![TextMagic Domain and URLs single sign-on information](./media/textmagic-tutorial/tutorial_textmagic_url.png)

    <span data-ttu-id="6c8ef-155">In the **Identifier** textbox, type a URL: `https://my.textmagic.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="6c8ef-155">In the **Identifier** textbox, type a URL: `https://my.textmagic.com/saml/metadata`</span></span>

1. <span data-ttu-id="6c8ef-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="6c8ef-156">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![TextMagic Domain and URLs single sign-on information](./media/textmagic-tutorial/url1.png)

    <span data-ttu-id="6c8ef-158">In the **Sign-on URL** textbox, type a URL: `https://my.textmagic.com/login/sso`</span><span class="sxs-lookup"><span data-stu-id="6c8ef-158">In the **Sign-on URL** textbox, type a URL: `https://my.textmagic.com/login/sso`</span></span>


1. <span data-ttu-id="6c8ef-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/textmagic-tutorial/tutorial_textmagic_certificate.png) 

1. <span data-ttu-id="6c8ef-161">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-161">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/textmagic-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="6c8ef-163">On the **TextMagic Configuration** section, click **Configure TextMagic** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-163">On the **TextMagic Configuration** section, click **Configure TextMagic** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6c8ef-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="6c8ef-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![TextMagic Configuration](./media/textmagic-tutorial/tutorial_textmagic_configure.png) 

1. <span data-ttu-id="6c8ef-166">In a different web browser window, log in to your TextMagic company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-166">In a different web browser window, log in to your TextMagic company site as an administrator.</span></span>

1. <span data-ttu-id="6c8ef-167">Select **Account settings** under the username.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-167">Select **Account settings** under the username.</span></span>

    ![TextMagic Configuration](./media/textmagic-tutorial/config1.png) 
1. <span data-ttu-id="6c8ef-169">Click on the TAB  **“Single Sign-On (SSO)”** and fill in the following fields:</span><span class="sxs-lookup"><span data-stu-id="6c8ef-169">Click on the TAB  **“Single Sign-On (SSO)”** and fill in the following fields:</span></span>  
    
    ![TextMagic Configuration](./media/textmagic-tutorial/config2.png)

    <span data-ttu-id="6c8ef-171">a.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-171">a.</span></span> <span data-ttu-id="6c8ef-172">In **Identity provider Entity ID:** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-172">In **Identity provider Entity ID:** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6c8ef-173">b.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-173">b.</span></span> <span data-ttu-id="6c8ef-174">In **Identity provider SSO URL:** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-174">In **Identity provider SSO URL:** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6c8ef-175">c.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-175">c.</span></span> <span data-ttu-id="6c8ef-176">In **Identity provider SLO URL:** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-176">In **Identity provider SLO URL:** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6c8ef-177">d.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-177">d.</span></span> <span data-ttu-id="6c8ef-178">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Public x509 certificate:** textbox.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-178">Open your **base-64 encoded certificate** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Public x509 certificate:** textbox.</span></span>

    <span data-ttu-id="6c8ef-179">e.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-179">e.</span></span> <span data-ttu-id="6c8ef-180">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-180">Click **Save**.</span></span>


> [!TIP]
> <span data-ttu-id="6c8ef-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="6c8ef-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6c8ef-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6c8ef-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6c8ef-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6c8ef-184">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6c8ef-184">Create an Azure AD test user</span></span>

<span data-ttu-id="6c8ef-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="6c8ef-187">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6c8ef-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6c8ef-188">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-188">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/textmagic-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="6c8ef-190">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-190">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/textmagic-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="6c8ef-192">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-192">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/textmagic-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="6c8ef-194">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6c8ef-194">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/textmagic-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6c8ef-196">a.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-196">a.</span></span> <span data-ttu-id="6c8ef-197">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-197">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6c8ef-198">b.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-198">b.</span></span> <span data-ttu-id="6c8ef-199">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-199">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="6c8ef-200">c.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-200">c.</span></span> <span data-ttu-id="6c8ef-201">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-201">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="6c8ef-202">d.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-202">d.</span></span> <span data-ttu-id="6c8ef-203">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-203">Click **Create**.</span></span>
 
### <a name="create-a-textmagic-test-user"></a><span data-ttu-id="6c8ef-204">Create a TextMagic test user</span><span class="sxs-lookup"><span data-stu-id="6c8ef-204">Create a TextMagic test user</span></span>

<span data-ttu-id="6c8ef-205">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-205">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="6c8ef-206">You need to fill in the information once at the first login to activate the sub-account into the system.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-206">You need to fill in the information once at the first login to activate the sub-account into the system.</span></span>
<span data-ttu-id="6c8ef-207">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-207">There is no action item for you in this section.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6c8ef-208">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6c8ef-208">Assign the Azure AD test user</span></span>

<span data-ttu-id="6c8ef-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TextMagic.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TextMagic.</span></span>

![Assign the user role][200] 

<span data-ttu-id="6c8ef-211">**To assign Britta Simon to TextMagic, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6c8ef-211">**To assign Britta Simon to TextMagic, perform the following steps:**</span></span>

1. <span data-ttu-id="6c8ef-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="6c8ef-214">In the applications list, select **TextMagic**.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-214">In the applications list, select **TextMagic**.</span></span>

    ![The TextMagic link in the Applications list](./media/textmagic-tutorial/tutorial_textmagic_app.png)  

1. <span data-ttu-id="6c8ef-216">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-216">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="6c8ef-218">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-218">Click **Add** button.</span></span> <span data-ttu-id="6c8ef-219">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="6c8ef-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="6c8ef-222">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-222">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="6c8ef-223">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6c8ef-224">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="6c8ef-224">Test single sign-on</span></span>

<span data-ttu-id="6c8ef-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6c8ef-226">When you click the TextMagic tile in the Access Panel, you should get automatically signed-on to your TextMagic application.</span><span class="sxs-lookup"><span data-stu-id="6c8ef-226">When you click the TextMagic tile in the Access Panel, you should get automatically signed-on to your TextMagic application.</span></span>
<span data-ttu-id="6c8ef-227">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6c8ef-227">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6c8ef-228">Additional resources</span><span class="sxs-lookup"><span data-stu-id="6c8ef-228">Additional resources</span></span>

* [<span data-ttu-id="6c8ef-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6c8ef-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="6c8ef-230">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6c8ef-230">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/textmagic-tutorial/tutorial_general_01.png
[2]: ./media/textmagic-tutorial/tutorial_general_02.png
[3]: ./media/textmagic-tutorial/tutorial_general_03.png
[4]: ./media/textmagic-tutorial/tutorial_general_04.png

[100]: ./media/textmagic-tutorial/tutorial_general_100.png

[200]: ./media/textmagic-tutorial/tutorial_general_200.png
[201]: ./media/textmagic-tutorial/tutorial_general_201.png
[202]: ./media/textmagic-tutorial/tutorial_general_202.png
[203]: ./media/textmagic-tutorial/tutorial_general_203.png

