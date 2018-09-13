---
title: 'Tutorial: Azure Active Directory integration with Teamphoria | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Teamphoria.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2018
ms.author: jeedes
ms.openlocfilehash: 554930b18a271a677aeb5e82c3e62a94965a8e7f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869028"
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="a37f7-103">Tutorial: Azure Active Directory integration with Teamphoria</span><span class="sxs-lookup"><span data-stu-id="a37f7-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="a37f7-104">In this tutorial, you learn how to integrate Teamphoria with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a37f7-104">In this tutorial, you learn how to integrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a37f7-105">Integrating Teamphoria with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a37f7-105">Integrating Teamphoria with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a37f7-106">You can control in Azure AD who has access to Teamphoria</span><span class="sxs-lookup"><span data-stu-id="a37f7-106">You can control in Azure AD who has access to Teamphoria</span></span>
- <span data-ttu-id="a37f7-107">You can enable your users to automatically get signed-on to Teamphoria (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="a37f7-107">You can enable your users to automatically get signed-on to Teamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a37f7-108">You can manage your accounts in one central location - the Azure  portal</span><span class="sxs-lookup"><span data-stu-id="a37f7-108">You can manage your accounts in one central location - the Azure  portal</span></span>

<span data-ttu-id="a37f7-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a37f7-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a37f7-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a37f7-110">Prerequisites</span></span>

<span data-ttu-id="a37f7-111">To configure Azure AD integration with Teamphoria, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a37f7-111">To configure Azure AD integration with Teamphoria, you need the following items:</span></span>

- <span data-ttu-id="a37f7-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a37f7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a37f7-113">A Teamphoria single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a37f7-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a37f7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a37f7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a37f7-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a37f7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a37f7-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a37f7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a37f7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a37f7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a37f7-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a37f7-118">Scenario description</span></span>
<span data-ttu-id="a37f7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a37f7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>
<span data-ttu-id="a37f7-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a37f7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a37f7-121">Adding Teamphoria from the gallery</span><span class="sxs-lookup"><span data-stu-id="a37f7-121">Adding Teamphoria from the gallery</span></span>
1. <span data-ttu-id="a37f7-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a37f7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-the-gallery"></a><span data-ttu-id="a37f7-123">Adding Teamphoria from the gallery</span><span class="sxs-lookup"><span data-stu-id="a37f7-123">Adding Teamphoria from the gallery</span></span>
<span data-ttu-id="a37f7-124">To configure the integration of Teamphoria into Azure AD, you need to add Teamphoria from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a37f7-124">To configure the integration of Teamphoria into Azure AD, you need to add Teamphoria from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a37f7-125">**To add Teamphoria from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a37f7-125">**To add Teamphoria from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a37f7-126">In the **[Azure  Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a37f7-126">In the **[Azure  Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span>

    ![Active Directory][1]

1. <span data-ttu-id="a37f7-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a37f7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a37f7-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a37f7-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="a37f7-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="a37f7-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="a37f7-133">In the search box, type **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="a37f7-133">In the search box, type **Teamphoria**.</span></span>

    ![Creating an Azure AD test user](./media/teamphoria-tutorial/tutorial_teamphoria_search.png)

1. <span data-ttu-id="a37f7-135">In the results panel, select **Teamphoria**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a37f7-135">In the results panel, select **Teamphoria**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a37f7-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a37f7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a37f7-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="a37f7-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a37f7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamphoria is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a37f7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Teamphoria is to a user in Azure AD.</span></span> <span data-ttu-id="a37f7-140">In other words, a link relationship between an Azure AD user and the related user in Teamphoria needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a37f7-140">In other words, a link relationship between an Azure AD user and the related user in Teamphoria needs to be established.</span></span>

<span data-ttu-id="a37f7-141">To configure and test Azure AD single sign-on with Teamphoria, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a37f7-141">To configure and test Azure AD single sign-on with Teamphoria, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a37f7-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a37f7-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="a37f7-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a37f7-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="a37f7-144">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - to have a counterpart of Britta Simon in Teamphoria that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="a37f7-144">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - to have a counterpart of Britta Simon in Teamphoria that is linked to the Azure AD representation of her.</span></span>
1. <span data-ttu-id="a37f7-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a37f7-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="a37f7-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a37f7-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a37f7-147">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a37f7-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a37f7-148">In this section, you enable Azure AD single sign-on in the Azure  portal and configure single sign-on in your Teamphoria application.</span><span class="sxs-lookup"><span data-stu-id="a37f7-148">In this section, you enable Azure AD single sign-on in the Azure  portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="a37f7-149">**To configure Azure AD single sign-on with Teamphoria, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a37f7-149">**To configure Azure AD single sign-on with Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="a37f7-150">In the Azure  portal, on the **Teamphoria** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a37f7-150">In the Azure  portal, on the **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="a37f7-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a37f7-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configure Single Sign-On](./media/teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

1. <span data-ttu-id="a37f7-154">On the **Teamphoria Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a37f7-154">On the **Teamphoria Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="a37f7-156">In the **Sign-on URL** textbox, type the URL using the following pattern: `https://<sub-domain>.teamphoria.com/login`</span><span class="sxs-lookup"><span data-stu-id="a37f7-156">In the **Sign-on URL** textbox, type the URL using the following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>   

    > [!NOTE] 
    > <span data-ttu-id="a37f7-157">The Sign-On URL value is not real.</span><span class="sxs-lookup"><span data-stu-id="a37f7-157">The Sign-On URL value is not real.</span></span> <span data-ttu-id="a37f7-158">You have to update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="a37f7-158">You have to update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="a37f7-159">Contact [Teamphoria Client support team](https://www.teamphoria.com/) to get the Sign-on URL.</span><span class="sxs-lookup"><span data-stu-id="a37f7-159">Contact [Teamphoria Client support team](https://www.teamphoria.com/) to get the Sign-on URL.</span></span>

1. <span data-ttu-id="a37f7-160">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate on your computer.</span><span class="sxs-lookup"><span data-stu-id="a37f7-160">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate on your computer.</span></span>

    ![Configure Single Sign-On](./media/teamphoria-tutorial/tutorial_teamphoria_certificate.png)

1. <span data-ttu-id="a37f7-162">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a37f7-162">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/teamphoria-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="a37f7-164">On the **Teamphoria Configuration** section, click **Configure Teamphoria** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="a37f7-164">On the **Teamphoria Configuration** section, click **Configure Teamphoria** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a37f7-165">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="a37f7-165">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/teamphoria-tutorial/tutorial_teamphoria_configure.png)

1. <span data-ttu-id="a37f7-167">To configure single sign-on on **Teamphoria** side, Login to your Teamphoria application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="a37f7-167">To configure single sign-on on **Teamphoria** side, Login to your Teamphoria application as an administrator.</span></span>

1. <span data-ttu-id="a37f7-168">Go to **ADMIN SETTINGS** option in the left toolbar and under the Configure Tab click on **SINGLE SIGN-ON** to open the SSO configuration window.</span><span class="sxs-lookup"><span data-stu-id="a37f7-168">Go to **ADMIN SETTINGS** option in the left toolbar and under the Configure Tab click on **SINGLE SIGN-ON** to open the SSO configuration window.</span></span>

    ![Configure Single Sign-On](./media/teamphoria-tutorial/admin_sso_configure.png)

1. <span data-ttu-id="a37f7-170">Click on **ADD NEW IDENTITY PROVIDER** option in the top right corner to open the form for adding the settings for SSO.</span><span class="sxs-lookup"><span data-stu-id="a37f7-170">Click on **ADD NEW IDENTITY PROVIDER** option in the top right corner to open the form for adding the settings for SSO.</span></span>

    ![Configure Single Sign-On](./media/teamphoria-tutorial/add_new_identity_provider.png)

1. <span data-ttu-id="a37f7-172">Enter the details in the fields as described below-</span><span class="sxs-lookup"><span data-stu-id="a37f7-172">Enter the details in the fields as described below-</span></span>

    ![Configure Single Sign-On](./media/teamphoria-tutorial/Teamphoria_sso_save.png)

    <span data-ttu-id="a37f7-174">a.</span><span class="sxs-lookup"><span data-stu-id="a37f7-174">a.</span></span> <span data-ttu-id="a37f7-175">**DISPLAY NAME**: Enter the display name of the plugin on the admin page.</span><span class="sxs-lookup"><span data-stu-id="a37f7-175">**DISPLAY NAME**: Enter the display name of the plugin on the admin page.</span></span>

    <span data-ttu-id="a37f7-176">b.</span><span class="sxs-lookup"><span data-stu-id="a37f7-176">b.</span></span> <span data-ttu-id="a37f7-177">**BUTTON NAME**: The name of the tab that will display on the login page for logging in via SSO.</span><span class="sxs-lookup"><span data-stu-id="a37f7-177">**BUTTON NAME**: The name of the tab that will display on the login page for logging in via SSO.</span></span>

    <span data-ttu-id="a37f7-178">c.</span><span class="sxs-lookup"><span data-stu-id="a37f7-178">c.</span></span> <span data-ttu-id="a37f7-179">**CERTIFICATE**: Open the Certificate downloaded earlier from the Azure portal in notepad, copy the contents of the same and paste it here in the box.</span><span class="sxs-lookup"><span data-stu-id="a37f7-179">**CERTIFICATE**: Open the Certificate downloaded earlier from the Azure portal in notepad, copy the contents of the same and paste it here in the box.</span></span>

    <span data-ttu-id="a37f7-180">d.</span><span class="sxs-lookup"><span data-stu-id="a37f7-180">d.</span></span> <span data-ttu-id="a37f7-181">**ENTRY POINT**: Paste the **SAML Single Sign-On Service URL** copied earlier from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a37f7-181">**ENTRY POINT**: Paste the **SAML Single Sign-On Service URL** copied earlier from the Azure portal.</span></span>

    <span data-ttu-id="a37f7-182">e.</span><span class="sxs-lookup"><span data-stu-id="a37f7-182">e.</span></span> <span data-ttu-id="a37f7-183">Switch the option to **ON** and click on **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="a37f7-183">Switch the option to **ON** and click on **SAVE**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a37f7-184">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a37f7-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="a37f7-185">The objective of this section is to create a test user in the Azure  portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a37f7-185">The objective of this section is to create a test user in the Azure  portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="a37f7-187">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a37f7-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a37f7-188">In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a37f7-188">In the **Azure  portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/teamphoria-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="a37f7-190">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a37f7-190">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Creating an Azure AD test user](./media/teamphoria-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="a37f7-192">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="a37f7-192">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/teamphoria-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="a37f7-194">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a37f7-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a37f7-196">a.</span><span class="sxs-lookup"><span data-stu-id="a37f7-196">a.</span></span> <span data-ttu-id="a37f7-197">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a37f7-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a37f7-198">b.</span><span class="sxs-lookup"><span data-stu-id="a37f7-198">b.</span></span> <span data-ttu-id="a37f7-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a37f7-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a37f7-200">c.</span><span class="sxs-lookup"><span data-stu-id="a37f7-200">c.</span></span> <span data-ttu-id="a37f7-201">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="a37f7-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a37f7-202">d.</span><span class="sxs-lookup"><span data-stu-id="a37f7-202">d.</span></span> <span data-ttu-id="a37f7-203">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a37f7-203">Click **Create**.</span></span>

### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="a37f7-204">Creating a Teamphoria test user</span><span class="sxs-lookup"><span data-stu-id="a37f7-204">Creating a Teamphoria test user</span></span>

<span data-ttu-id="a37f7-205">In order to enable Azure AD users to log into Teamphoria, they must be provisioned into Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="a37f7-205">In order to enable Azure AD users to log into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="a37f7-206">In the case of Teamphoria, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="a37f7-206">In the case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="a37f7-207">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a37f7-207">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="a37f7-208">Log in to your Teamphoria company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="a37f7-208">Log in to your Teamphoria company site as an administrator.</span></span>

1. <span data-ttu-id="a37f7-209">Click on **ADMIN** settings on the left toolbar and under the **MANAGE** tab Click on **USERS** to open the admin page for users.</span><span class="sxs-lookup"><span data-stu-id="a37f7-209">Click on **ADMIN** settings on the left toolbar and under the **MANAGE** tab Click on **USERS** to open the admin page for users.</span></span>

    ![Add Employee](./media/teamphoria-tutorial/admin_manage_users.png)

1. <span data-ttu-id="a37f7-211">Click on the **MANUAL INVITE** option.</span><span class="sxs-lookup"><span data-stu-id="a37f7-211">Click on the **MANUAL INVITE** option.</span></span>

    ![Invite People](./media/teamphoria-tutorial/admin_manage_add_users.png)

1. <span data-ttu-id="a37f7-213">On this page, perform following action.</span><span class="sxs-lookup"><span data-stu-id="a37f7-213">On this page, perform following action.</span></span>
    
    ![Invite People](./media/teamphoria-tutorial/manual_user_invite.png)

    <span data-ttu-id="a37f7-215">a.</span><span class="sxs-lookup"><span data-stu-id="a37f7-215">a.</span></span> <span data-ttu-id="a37f7-216">In the **EMAIL ADDRESS** textbox, the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a37f7-216">In the **EMAIL ADDRESS** textbox, the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a37f7-217">b.</span><span class="sxs-lookup"><span data-stu-id="a37f7-217">b.</span></span> <span data-ttu-id="a37f7-218">In the **FIRST NAME** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a37f7-218">In the **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="a37f7-219">c.</span><span class="sxs-lookup"><span data-stu-id="a37f7-219">c.</span></span> <span data-ttu-id="a37f7-220">In the **LAST NAME** textbox, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="a37f7-220">In the **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="a37f7-221">d.</span><span class="sxs-lookup"><span data-stu-id="a37f7-221">d.</span></span> <span data-ttu-id="a37f7-222">Click **INVITE 1 USER**.</span><span class="sxs-lookup"><span data-stu-id="a37f7-222">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="a37f7-223">User needs to accept the invite to get created in the system.</span><span class="sxs-lookup"><span data-stu-id="a37f7-223">User needs to accept the invite to get created in the system.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a37f7-224">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a37f7-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a37f7-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="a37f7-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Teamphoria.</span></span>

![Assign User][200]

<span data-ttu-id="a37f7-227">**To assign Britta Simon to Teamphoria, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a37f7-227">**To assign Britta Simon to Teamphoria, perform the following steps:**</span></span>

1. <span data-ttu-id="a37f7-228">In the Azure  portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a37f7-228">In the Azure  portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

1. <span data-ttu-id="a37f7-230">In the applications list, select **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="a37f7-230">In the applications list, select **Teamphoria**.</span></span>

    ![Configure Single Sign-On](./media/teamphoria-tutorial/tutorial_teamphoria_app.png) 

1. <span data-ttu-id="a37f7-232">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a37f7-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202]

1. <span data-ttu-id="a37f7-234">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a37f7-234">Click **Add** button.</span></span> <span data-ttu-id="a37f7-235">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a37f7-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="a37f7-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a37f7-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="a37f7-238">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a37f7-238">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="a37f7-239">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a37f7-239">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="a37f7-240">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="a37f7-240">Testing single sign-on</span></span>

<span data-ttu-id="a37f7-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a37f7-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a37f7-242">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a37f7-242">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="a37f7-243">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a37f7-243">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a37f7-244">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a37f7-244">Additional resources</span></span>

* [<span data-ttu-id="a37f7-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a37f7-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a37f7-246">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a37f7-246">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/teamphoria-tutorial/tutorial_general_203.png
