---
title: 'Tutorial: Azure Active Directory integration with Jive | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Jive.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 9fc5659a-c116-4a1b-a601-333325a26b46
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2018
ms.author: jeedes
ms.openlocfilehash: cebcfb4614d1f685697bed6914f80237e175fb7b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871003"
---
# <a name="tutorial-azure-active-directory-integration-with-jive"></a><span data-ttu-id="8153a-103">Tutorial: Azure Active Directory integration with Jive</span><span class="sxs-lookup"><span data-stu-id="8153a-103">Tutorial: Azure Active Directory integration with Jive</span></span>

<span data-ttu-id="8153a-104">In this tutorial, you learn how to integrate Jive with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8153a-104">In this tutorial, you learn how to integrate Jive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8153a-105">Integrating Jive with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8153a-105">Integrating Jive with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8153a-106">You can control in Azure AD who has access to Jive</span><span class="sxs-lookup"><span data-stu-id="8153a-106">You can control in Azure AD who has access to Jive</span></span>
- <span data-ttu-id="8153a-107">You can enable your users to automatically get signed-on to Jive (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="8153a-107">You can enable your users to automatically get signed-on to Jive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8153a-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8153a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8153a-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="8153a-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8153a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8153a-110">Prerequisites</span></span>

<span data-ttu-id="8153a-111">To configure Azure AD integration with Jive, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8153a-111">To configure Azure AD integration with Jive, you need the following items:</span></span>

- <span data-ttu-id="8153a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8153a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8153a-113">A Jive single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8153a-113">A Jive single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8153a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8153a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8153a-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8153a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8153a-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="8153a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8153a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8153a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8153a-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="8153a-118">Scenario description</span></span>
<span data-ttu-id="8153a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8153a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>
<span data-ttu-id="8153a-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8153a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8153a-121">Adding Jive from the gallery</span><span class="sxs-lookup"><span data-stu-id="8153a-121">Adding Jive from the gallery</span></span>
1. <span data-ttu-id="8153a-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8153a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jive-from-the-gallery"></a><span data-ttu-id="8153a-123">Adding Jive from the gallery</span><span class="sxs-lookup"><span data-stu-id="8153a-123">Adding Jive from the gallery</span></span>
<span data-ttu-id="8153a-124">To configure the integration of Jive into Azure AD, you need to add Jive from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8153a-124">To configure the integration of Jive into Azure AD, you need to add Jive from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8153a-125">**To add Jive from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8153a-125">**To add Jive from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8153a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8153a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="8153a-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="8153a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8153a-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8153a-129">Then go to **All applications**.</span></span>

    ![Applications][2]

1. <span data-ttu-id="8153a-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="8153a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="8153a-133">In the search box, type **Jive**.</span><span class="sxs-lookup"><span data-stu-id="8153a-133">In the search box, type **Jive**.</span></span>

    ![Creating an Azure AD test user](./media/jive-tutorial/tutorial_jive_search.png)

1. <span data-ttu-id="8153a-135">In the results panel, select **Jive**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="8153a-135">In the results panel, select **Jive**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/jive-tutorial/tutorial_jive_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8153a-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8153a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8153a-138">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="8153a-138">In this section, you configure and test Azure AD single sign-on with Jive based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8153a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jive is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8153a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jive is to a user in Azure AD.</span></span> <span data-ttu-id="8153a-140">In other words, a link relationship between an Azure AD user and the related user in Jive needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8153a-140">In other words, a link relationship between an Azure AD user and the related user in Jive needs to be established.</span></span>

<span data-ttu-id="8153a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Jive.</span><span class="sxs-lookup"><span data-stu-id="8153a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Jive.</span></span>

<span data-ttu-id="8153a-142">To configure and test Azure AD single sign-on with Jive, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8153a-142">To configure and test Azure AD single sign-on with Jive, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8153a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8153a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="8153a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8153a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="8153a-145">**[Creating a Jive test user](#creating-a-jive-test-user)** - to have a counterpart of Britta Simon in Jive that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="8153a-145">**[Creating a Jive test user](#creating-a-jive-test-user)** - to have a counterpart of Britta Simon in Jive that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="8153a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8153a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="8153a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8153a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8153a-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8153a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8153a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jive application.</span><span class="sxs-lookup"><span data-stu-id="8153a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jive application.</span></span>

<span data-ttu-id="8153a-150">**To configure Azure AD single sign-on with Jive, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8153a-150">**To configure Azure AD single sign-on with Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="8153a-151">In the Azure portal, on the **Jive** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8153a-151">In the Azure portal, on the **Jive** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="8153a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8153a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Configure Single Sign-On](./media/jive-tutorial/tutorial_jive_samlbase.png)

1. <span data-ttu-id="8153a-155">On the **Jive Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8153a-155">On the **Jive Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/jive-tutorial/tutorial_jive_url.png)

    <span data-ttu-id="8153a-157">a.</span><span class="sxs-lookup"><span data-stu-id="8153a-157">a.</span></span> <span data-ttu-id="8153a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance name>.jivecustom.com`</span><span class="sxs-lookup"><span data-stu-id="8153a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instance name>.jivecustom.com`</span></span>

    <span data-ttu-id="8153a-159">b.</span><span class="sxs-lookup"><span data-stu-id="8153a-159">b.</span></span> <span data-ttu-id="8153a-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance name>.jiveon.com`</span><span class="sxs-lookup"><span data-stu-id="8153a-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance name>.jiveon.com`</span></span>

    > [!NOTE]
    > <span data-ttu-id="8153a-161">These values are not the real.</span><span class="sxs-lookup"><span data-stu-id="8153a-161">These values are not the real.</span></span> <span data-ttu-id="8153a-162">Update these values with the actual Sign-on URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="8153a-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="8153a-163">Contact [Jive Client support team](https://www.jivesoftware.com/services-support/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="8153a-163">Contact [Jive Client support team](https://www.jivesoftware.com/services-support/) to get these values.</span></span>

1. <span data-ttu-id="8153a-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8153a-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](./media/jive-tutorial/tutorial_jive_certificate.png)

1. <span data-ttu-id="8153a-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="8153a-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/jive-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="8153a-168">To configure single sign-on on **Jive** side, sign-on to your Jive tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="8153a-168">To configure single sign-on on **Jive** side, sign-on to your Jive tenant as an administrator.</span></span>

1. <span data-ttu-id="8153a-169">In the menu on the top, Click "**Saml**."</span><span class="sxs-lookup"><span data-stu-id="8153a-169">In the menu on the top, Click "**Saml**."</span></span>

    ![Configure Single Sign-On On App Side](./media/jive-tutorial/tutorial_jive_002.png)

    <span data-ttu-id="8153a-171">a.</span><span class="sxs-lookup"><span data-stu-id="8153a-171">a.</span></span> <span data-ttu-id="8153a-172">Select **Enabled** under the **General** tab. b.</span><span class="sxs-lookup"><span data-stu-id="8153a-172">Select **Enabled** under the **General** tab. b.</span></span> <span data-ttu-id="8153a-173">Click the "**Save all saml settings**" button.</span><span class="sxs-lookup"><span data-stu-id="8153a-173">Click the "**Save all saml settings**" button.</span></span>

1. <span data-ttu-id="8153a-174">Navigate to the "**Idp Metadata**" tab.</span><span class="sxs-lookup"><span data-stu-id="8153a-174">Navigate to the "**Idp Metadata**" tab.</span></span>

    ![Configure Single Sign-On On App Side](./media/jive-tutorial/tutorial_jive_003.png)

    <span data-ttu-id="8153a-176">a.</span><span class="sxs-lookup"><span data-stu-id="8153a-176">a.</span></span> <span data-ttu-id="8153a-177">Copy the content of the downloaded metadata XML file, and then paste it into the **Identity Provider (IDP) Metadata** textbox.</span><span class="sxs-lookup"><span data-stu-id="8153a-177">Copy the content of the downloaded metadata XML file, and then paste it into the **Identity Provider (IDP) Metadata** textbox.</span></span>

    <span data-ttu-id="8153a-178">b.</span><span class="sxs-lookup"><span data-stu-id="8153a-178">b.</span></span> <span data-ttu-id="8153a-179">Click the "**Save all saml settings**" button.</span><span class="sxs-lookup"><span data-stu-id="8153a-179">Click the "**Save all saml settings**" button.</span></span>

1. <span data-ttu-id="8153a-180">Go to the "**User Attribute Mapping**" tab.</span><span class="sxs-lookup"><span data-stu-id="8153a-180">Go to the "**User Attribute Mapping**" tab.</span></span>

    ![Configure Single Sign-On On App Side](./media/jive-tutorial/tutorial_jive_004.png)

    <span data-ttu-id="8153a-182">a.</span><span class="sxs-lookup"><span data-stu-id="8153a-182">a.</span></span> <span data-ttu-id="8153a-183">In the **Email** textbox, copy and paste the attribute name of **mail** value.</span><span class="sxs-lookup"><span data-stu-id="8153a-183">In the **Email** textbox, copy and paste the attribute name of **mail** value.</span></span>

    <span data-ttu-id="8153a-184">b.</span><span class="sxs-lookup"><span data-stu-id="8153a-184">b.</span></span> <span data-ttu-id="8153a-185">In the **First Name** textbox, copy and paste the attribute name of **givenname** value.</span><span class="sxs-lookup"><span data-stu-id="8153a-185">In the **First Name** textbox, copy and paste the attribute name of **givenname** value.</span></span>

    <span data-ttu-id="8153a-186">c.</span><span class="sxs-lookup"><span data-stu-id="8153a-186">c.</span></span> <span data-ttu-id="8153a-187">In the **Last Name** textbox, copy and paste the attribute name of **surname** value.</span><span class="sxs-lookup"><span data-stu-id="8153a-187">In the **Last Name** textbox, copy and paste the attribute name of **surname** value.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8153a-188">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8153a-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="8153a-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8153a-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="8153a-191">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8153a-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8153a-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8153a-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/jive-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="8153a-194">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="8153a-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>

    ![Creating an Azure AD test user](./media/jive-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="8153a-196">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="8153a-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>

    ![Creating an Azure AD test user](./media/jive-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="8153a-198">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8153a-198">On the **User** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](./media/jive-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8153a-200">a.</span><span class="sxs-lookup"><span data-stu-id="8153a-200">a.</span></span> <span data-ttu-id="8153a-201">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8153a-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8153a-202">b.</span><span class="sxs-lookup"><span data-stu-id="8153a-202">b.</span></span> <span data-ttu-id="8153a-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8153a-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8153a-204">c.</span><span class="sxs-lookup"><span data-stu-id="8153a-204">c.</span></span> <span data-ttu-id="8153a-205">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="8153a-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8153a-206">d.</span><span class="sxs-lookup"><span data-stu-id="8153a-206">d.</span></span> <span data-ttu-id="8153a-207">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8153a-207">Click **Create**.</span></span>

### <a name="creating-a-jive-test-user"></a><span data-ttu-id="8153a-208">Creating a Jive test user</span><span class="sxs-lookup"><span data-stu-id="8153a-208">Creating a Jive test user</span></span>

<span data-ttu-id="8153a-209">The objective of this section is to create a user called Britta Simon in Jive.</span><span class="sxs-lookup"><span data-stu-id="8153a-209">The objective of this section is to create a user called Britta Simon in Jive.</span></span> <span data-ttu-id="8153a-210">Jive supports automatic user provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="8153a-210">Jive supports automatic user provisioning, which is by default enabled.</span></span> <span data-ttu-id="8153a-211">You can find more details [here](jive-provisioning-tutorial.md) on how to configure automatic user provisioning.</span><span class="sxs-lookup"><span data-stu-id="8153a-211">You can find more details [here](jive-provisioning-tutorial.md) on how to configure automatic user provisioning.</span></span>

<span data-ttu-id="8153a-212">If you need to create user manually, work with [Jive Client support team](https://www.jivesoftware.com/services-support/) to add the users in the Jive platform.</span><span class="sxs-lookup"><span data-stu-id="8153a-212">If you need to create user manually, work with [Jive Client support team](https://www.jivesoftware.com/services-support/) to add the users in the Jive platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8153a-213">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8153a-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8153a-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jive.</span><span class="sxs-lookup"><span data-stu-id="8153a-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jive.</span></span>

![Assign User][200] 

<span data-ttu-id="8153a-216">**To assign Britta Simon to Jive, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8153a-216">**To assign Britta Simon to Jive, perform the following steps:**</span></span>

1. <span data-ttu-id="8153a-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8153a-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="8153a-219">In the applications list, select **Jive**.</span><span class="sxs-lookup"><span data-stu-id="8153a-219">In the applications list, select **Jive**.</span></span>

    ![Configure Single Sign-On](./media/jive-tutorial/tutorial_jive_app.png) 

1. <span data-ttu-id="8153a-221">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="8153a-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="8153a-223">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="8153a-223">Click **Add** button.</span></span> <span data-ttu-id="8153a-224">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8153a-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="8153a-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="8153a-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="8153a-227">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="8153a-227">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="8153a-228">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8153a-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8153a-229">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="8153a-229">Testing single sign-on</span></span>

<span data-ttu-id="8153a-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8153a-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8153a-231">When you click the Jive tile in the Access Panel, you should get automatically signed-on to your Jive application.</span><span class="sxs-lookup"><span data-stu-id="8153a-231">When you click the Jive tile in the Access Panel, you should get automatically signed-on to your Jive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8153a-232">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8153a-232">Additional resources</span></span>

* [<span data-ttu-id="8153a-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8153a-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="8153a-234">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8153a-234">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)
* [<span data-ttu-id="8153a-235">Configure User Provisioning</span><span class="sxs-lookup"><span data-stu-id="8153a-235">Configure User Provisioning</span></span>](jive-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/jive-tutorial/tutorial_general_01.png
[2]: ./media/jive-tutorial/tutorial_general_02.png
[3]: ./media/jive-tutorial/tutorial_general_03.png
[4]: ./media/jive-tutorial/tutorial_general_04.png

[100]: ./media/jive-tutorial/tutorial_general_100.png

[200]: ./media/jive-tutorial/tutorial_general_200.png
[201]: ./media/jive-tutorial/tutorial_general_201.png
[202]: ./media/jive-tutorial/tutorial_general_202.png
[203]: ./media/jive-tutorial/tutorial_general_203.png
