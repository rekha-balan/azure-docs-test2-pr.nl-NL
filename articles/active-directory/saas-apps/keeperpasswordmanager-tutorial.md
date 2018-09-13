---
title: 'Tutorial: Azure Active Directory integration with Keeper Password Manager & Digital Vault | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Keeper Password Manager & Digital Vault.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: e1a98f6a-2dae-4734-bdbf-4fba742a61d2
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: dee9b81b6830244dec6860da0618d20c7f062ac2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857008"
---
# <a name="tutorial-azure-active-directory-integration-with-keeper-password-manager--digital-vault"></a><span data-ttu-id="72757-103">Tutorial: Azure Active Directory integration with Keeper Password Manager & Digital Vault</span><span class="sxs-lookup"><span data-stu-id="72757-103">Tutorial: Azure Active Directory integration with Keeper Password Manager & Digital Vault</span></span>

<span data-ttu-id="72757-104">In this tutorial, you learn how to integrate Keeper Password Manager & Digital Vault with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="72757-104">In this tutorial, you learn how to integrate Keeper Password Manager & Digital Vault with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="72757-105">Integrating Keeper Password Manager & Digital Vault with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="72757-105">Integrating Keeper Password Manager & Digital Vault with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="72757-106">You can control in Azure AD who has access to Keeper Password Manager & Digital Vault</span><span class="sxs-lookup"><span data-stu-id="72757-106">You can control in Azure AD who has access to Keeper Password Manager & Digital Vault</span></span>
- <span data-ttu-id="72757-107">You can enable your users to automatically get signed-on to Keeper Password Manager & Digital Vault (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="72757-107">You can enable your users to automatically get signed-on to Keeper Password Manager & Digital Vault (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="72757-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="72757-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="72757-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="72757-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72757-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="72757-110">Prerequisites</span></span>

<span data-ttu-id="72757-111">To configure Azure AD integration with Keeper Password Manager & Digital Vault, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="72757-111">To configure Azure AD integration with Keeper Password Manager & Digital Vault, you need the following items:</span></span>

- <span data-ttu-id="72757-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="72757-112">An Azure AD subscription</span></span>
- <span data-ttu-id="72757-113">A Keeper Password Manager & Digital Vault single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="72757-113">A Keeper Password Manager & Digital Vault single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="72757-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="72757-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="72757-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="72757-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="72757-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="72757-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="72757-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="72757-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="72757-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="72757-118">Scenario description</span></span>
<span data-ttu-id="72757-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="72757-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="72757-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="72757-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="72757-121">Adding Keeper Password Manager & Digital Vault from the gallery</span><span class="sxs-lookup"><span data-stu-id="72757-121">Adding Keeper Password Manager & Digital Vault from the gallery</span></span>
1. <span data-ttu-id="72757-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="72757-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-keeper-password-manager--digital-vault-from-the-gallery"></a><span data-ttu-id="72757-123">Adding Keeper Password Manager & Digital Vault from the gallery</span><span class="sxs-lookup"><span data-stu-id="72757-123">Adding Keeper Password Manager & Digital Vault from the gallery</span></span>
<span data-ttu-id="72757-124">To configure the integration of Keeper Password Manager & Digital Vault into Azure AD, you need to add Keeper Password Manager & Digital Vault from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="72757-124">To configure the integration of Keeper Password Manager & Digital Vault into Azure AD, you need to add Keeper Password Manager & Digital Vault from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="72757-125">**To add Keeper Password Manager & Digital Vault from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="72757-125">**To add Keeper Password Manager & Digital Vault from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="72757-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="72757-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="72757-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="72757-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="72757-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="72757-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="72757-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="72757-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="72757-133">In the search box, type **Keeper Password Manager & Digital Vault**.</span><span class="sxs-lookup"><span data-stu-id="72757-133">In the search box, type **Keeper Password Manager & Digital Vault**.</span></span>

    ![Creating an Azure AD test user](./media/keeperpasswordmanager-tutorial/tutorial_keeper_search.png)

1. <span data-ttu-id="72757-135">In the results panel, select **Keeper Password Manager & Digital Vault**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="72757-135">In the results panel, select **Keeper Password Manager & Digital Vault**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/keeperpasswordmanager-tutorial/tutorial_keeper_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="72757-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="72757-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="72757-138">In this section, you configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="72757-138">In this section, you configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="72757-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Keeper Password Manager & Digital Vault is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="72757-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Keeper Password Manager & Digital Vault is to a user in Azure AD.</span></span> <span data-ttu-id="72757-140">In other words, a link relationship between an Azure AD user and the related user in Keeper Password Manager & Digital Vault needs to be established.</span><span class="sxs-lookup"><span data-stu-id="72757-140">In other words, a link relationship between an Azure AD user and the related user in Keeper Password Manager & Digital Vault needs to be established.</span></span>

<span data-ttu-id="72757-141">In Keeper Password Manager & Digital Vault, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="72757-141">In Keeper Password Manager & Digital Vault, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="72757-142">To configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="72757-142">To configure and test Azure AD single sign-on with Keeper Password Manager & Digital Vault, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="72757-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="72757-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="72757-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="72757-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="72757-145">**[Creating a Keeper Password Manager & Digital Vault test user](#creating-a-keeperpasswordmanager-test-user)** - to have a counterpart of Britta Simon in Keeper Password Manager & Digital Vault that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="72757-145">**[Creating a Keeper Password Manager & Digital Vault test user](#creating-a-keeperpasswordmanager-test-user)** - to have a counterpart of Britta Simon in Keeper Password Manager & Digital Vault that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="72757-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="72757-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="72757-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="72757-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="72757-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="72757-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="72757-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Keeper Password Manager & Digital Vault application.</span><span class="sxs-lookup"><span data-stu-id="72757-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Keeper Password Manager & Digital Vault application.</span></span>

<span data-ttu-id="72757-150">**To configure Azure AD single sign-on with Keeper Password Manager & Digital Vault, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="72757-150">**To configure Azure AD single sign-on with Keeper Password Manager & Digital Vault, perform the following steps:**</span></span>

1. <span data-ttu-id="72757-151">In the Azure portal, on the **Keeper Password Manager & Digital Vault** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="72757-151">In the Azure portal, on the **Keeper Password Manager & Digital Vault** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="72757-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="72757-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/keeperpasswordmanager-tutorial/tutorial_keeper_samlbase.png)

1. <span data-ttu-id="72757-155">On the **Keeper Password Manager & Digital Vault Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="72757-155">On the **Keeper Password Manager & Digital Vault Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/keeperpasswordmanager-tutorial/tutorial_keeper_url.png)

    <span data-ttu-id="72757-157">a.</span><span class="sxs-lookup"><span data-stu-id="72757-157">a.</span></span> <span data-ttu-id="72757-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span><span class="sxs-lookup"><span data-stu-id="72757-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/login`</span></span>

    <span data-ttu-id="72757-159">b.</span><span class="sxs-lookup"><span data-stu-id="72757-159">b.</span></span> <span data-ttu-id="72757-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span><span class="sxs-lookup"><span data-stu-id="72757-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://{SSO CONNECT SERVER}/sso-connect/saml/sso`</span></span>

    <span data-ttu-id="72757-161">c.</span><span class="sxs-lookup"><span data-stu-id="72757-161">c.</span></span> <span data-ttu-id="72757-162">In the **Identifier** textbox, type a URL using the following pattern: `https://{SSO CONNECT SERVER}/sso-connect`</span><span class="sxs-lookup"><span data-stu-id="72757-162">In the **Identifier** textbox, type a URL using the following pattern: `https://{SSO CONNECT SERVER}/sso-connect`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="72757-163">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="72757-163">These values are not real.</span></span> <span data-ttu-id="72757-164">Update these values with the actual Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="72757-164">Update these values with the actual Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="72757-165">Contact [Keeper Password Manager & Digital Vault Client support team](https://keepersecurity.com/contact.html) to get these values.</span><span class="sxs-lookup"><span data-stu-id="72757-165">Contact [Keeper Password Manager & Digital Vault Client support team](https://keepersecurity.com/contact.html) to get these values.</span></span> 

1. <span data-ttu-id="72757-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="72757-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/keeperpasswordmanager-tutorial/tutorial_keeper_certificate.png) 

1. <span data-ttu-id="72757-168">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="72757-168">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/keeperpasswordmanager-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="72757-170">On the **Keeper Password Manager & Digital Vault Configuration** section, click **Configure Keeper Password Manager & Digital Vault** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="72757-170">On the **Keeper Password Manager & Digital Vault Configuration** section, click **Configure Keeper Password Manager & Digital Vault** to open **Configure sign-on** window.</span></span> <span data-ttu-id="72757-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="72757-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/keeperpasswordmanager-tutorial/tutorial_keeper_configure.png) 

1. <span data-ttu-id="72757-173">To configure single sign-on on **Keeper Password Manager & Digital Vault Configuration** side, follow the guidelines given at [Keeper Support Guide](https://keepersecurity.com/assets/pdf/KeeperSSOConnect_v11.pdf).</span><span class="sxs-lookup"><span data-stu-id="72757-173">To configure single sign-on on **Keeper Password Manager & Digital Vault Configuration** side, follow the guidelines given at [Keeper Support Guide](https://keepersecurity.com/assets/pdf/KeeperSSOConnect_v11.pdf).</span></span>

> [!TIP]
> <span data-ttu-id="72757-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="72757-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="72757-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="72757-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="72757-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="72757-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="72757-177">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="72757-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="72757-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="72757-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="72757-180">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="72757-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="72757-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="72757-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/keeperpasswordmanager-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="72757-183">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="72757-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/keeperpasswordmanager-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="72757-185">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="72757-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/keeperpasswordmanager-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="72757-187">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="72757-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/keeperpasswordmanager-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="72757-189">a.</span><span class="sxs-lookup"><span data-stu-id="72757-189">a.</span></span> <span data-ttu-id="72757-190">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="72757-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="72757-191">b.</span><span class="sxs-lookup"><span data-stu-id="72757-191">b.</span></span> <span data-ttu-id="72757-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="72757-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="72757-193">c.</span><span class="sxs-lookup"><span data-stu-id="72757-193">c.</span></span> <span data-ttu-id="72757-194">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="72757-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="72757-195">d.</span><span class="sxs-lookup"><span data-stu-id="72757-195">d.</span></span> <span data-ttu-id="72757-196">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="72757-196">Click **Create**.</span></span>
 
### <a name="creating-a-keeper-password-manager--digital-vault-test-user"></a><span data-ttu-id="72757-197">Creating a Keeper Password Manager & Digital Vault test user</span><span class="sxs-lookup"><span data-stu-id="72757-197">Creating a Keeper Password Manager & Digital Vault test user</span></span>

<span data-ttu-id="72757-198">To enable Azure AD users to log in to Keeper Password Manager & Digital Vault, they must be provisioned into Keeper Password Manager & Digital Vault.</span><span class="sxs-lookup"><span data-stu-id="72757-198">To enable Azure AD users to log in to Keeper Password Manager & Digital Vault, they must be provisioned into Keeper Password Manager & Digital Vault.</span></span> <span data-ttu-id="72757-199">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span><span class="sxs-lookup"><span data-stu-id="72757-199">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span> <span data-ttu-id="72757-200">You can contact [Keeper Support](https://keepersecurity.com/contact.html), if you want to setup users manually.</span><span class="sxs-lookup"><span data-stu-id="72757-200">You can contact [Keeper Support](https://keepersecurity.com/contact.html), if you want to setup users manually.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="72757-201">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="72757-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="72757-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Keeper Password Manager & Digital Vault.</span><span class="sxs-lookup"><span data-stu-id="72757-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Keeper Password Manager & Digital Vault.</span></span>

![Assign User][200] 

<span data-ttu-id="72757-204">**To assign Britta Simon to Keeper Password Manager & Digital Vault, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="72757-204">**To assign Britta Simon to Keeper Password Manager & Digital Vault, perform the following steps:**</span></span>

1. <span data-ttu-id="72757-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="72757-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="72757-207">In the applications list, select **Keeper Password Manager & Digital Vault**.</span><span class="sxs-lookup"><span data-stu-id="72757-207">In the applications list, select **Keeper Password Manager & Digital Vault**.</span></span>

    ![Configure Single Sign-On](./media/keeperpasswordmanager-tutorial/tutorial_keeper_app.png) 

1. <span data-ttu-id="72757-209">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="72757-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="72757-211">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="72757-211">Click **Add** button.</span></span> <span data-ttu-id="72757-212">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="72757-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="72757-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="72757-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="72757-215">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="72757-215">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="72757-216">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="72757-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="72757-217">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="72757-217">Testing single sign-on</span></span>

<span data-ttu-id="72757-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="72757-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="72757-219">When you click the Keeper Password Manager & Digital Vault tile in the Access Panel, you should get login page of Keeper Password Manager & Digital Vault application.</span><span class="sxs-lookup"><span data-stu-id="72757-219">When you click the Keeper Password Manager & Digital Vault tile in the Access Panel, you should get login page of Keeper Password Manager & Digital Vault application.</span></span> <span data-ttu-id="72757-220">Upon successful authentication, you should get into the application.</span><span class="sxs-lookup"><span data-stu-id="72757-220">Upon successful authentication, you should get into the application.</span></span> <span data-ttu-id="72757-221">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="72757-221">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="72757-222">Additional resources</span><span class="sxs-lookup"><span data-stu-id="72757-222">Additional resources</span></span>

* [<span data-ttu-id="72757-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="72757-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="72757-224">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="72757-224">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/keeperpasswordmanager-tutorial/tutorial_general_01.png
[2]: ./media/keeperpasswordmanager-tutorial/tutorial_general_02.png
[3]: ./media/keeperpasswordmanager-tutorial/tutorial_general_03.png
[4]: ./media/keeperpasswordmanager-tutorial/tutorial_general_04.png

[100]: ./media/keeperpasswordmanager-tutorial/tutorial_general_100.png

[200]: ./media/keeperpasswordmanager-tutorial/tutorial_general_200.png
[201]: ./media/keeperpasswordmanager-tutorial/tutorial_general_201.png
[202]: ./media/keeperpasswordmanager-tutorial/tutorial_general_202.png
[203]: ./media/keeperpasswordmanager-tutorial/tutorial_general_203.png

