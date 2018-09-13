---
title: 'Tutorial: Azure Active Directory integration with Heroku | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Heroku.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: d7d72ec6-4a60-4524-8634-26d8fbbcc833
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: c78d1207c724622fe16fa8d0a0717d71fbb6d37c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969071"
---
# <a name="tutorial-azure-active-directory-integration-with-heroku"></a><span data-ttu-id="43c43-103">Tutorial: Azure Active Directory integration with Heroku</span><span class="sxs-lookup"><span data-stu-id="43c43-103">Tutorial: Azure Active Directory integration with Heroku</span></span>

<span data-ttu-id="43c43-104">In this tutorial, you learn how to integrate Heroku with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="43c43-104">In this tutorial, you learn how to integrate Heroku with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="43c43-105">Integrating Heroku with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="43c43-105">Integrating Heroku with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="43c43-106">You can control in Azure AD who has access to Heroku</span><span class="sxs-lookup"><span data-stu-id="43c43-106">You can control in Azure AD who has access to Heroku</span></span>
- <span data-ttu-id="43c43-107">You can enable your users to automatically get signed-on to Heroku (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="43c43-107">You can enable your users to automatically get signed-on to Heroku (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="43c43-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="43c43-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="43c43-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="43c43-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="43c43-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="43c43-110">Prerequisites</span></span>

<span data-ttu-id="43c43-111">To configure Azure AD integration with Heroku, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="43c43-111">To configure Azure AD integration with Heroku, you need the following items:</span></span>

- <span data-ttu-id="43c43-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="43c43-112">An Azure AD subscription</span></span>
- <span data-ttu-id="43c43-113">A Heroku single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="43c43-113">A Heroku single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="43c43-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="43c43-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="43c43-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="43c43-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="43c43-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="43c43-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="43c43-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="43c43-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="43c43-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="43c43-118">Scenario description</span></span>
<span data-ttu-id="43c43-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="43c43-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="43c43-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="43c43-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="43c43-121">Adding Heroku from the gallery</span><span class="sxs-lookup"><span data-stu-id="43c43-121">Adding Heroku from the gallery</span></span>
1. <span data-ttu-id="43c43-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="43c43-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-heroku-from-the-gallery"></a><span data-ttu-id="43c43-123">Adding Heroku from the gallery</span><span class="sxs-lookup"><span data-stu-id="43c43-123">Adding Heroku from the gallery</span></span>
<span data-ttu-id="43c43-124">To configure the integration of Heroku into Azure AD, you need to add Heroku from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="43c43-124">To configure the integration of Heroku into Azure AD, you need to add Heroku from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="43c43-125">**To add Heroku from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="43c43-125">**To add Heroku from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="43c43-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="43c43-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="43c43-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="43c43-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="43c43-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="43c43-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="43c43-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="43c43-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="43c43-133">In the search box, type **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="43c43-133">In the search box, type **Heroku**.</span></span>

    ![Creating an Azure AD test user](./media/heroku-tutorial/tutorial_heroku_search.png)

1. <span data-ttu-id="43c43-135">In the results panel, select **Heroku**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="43c43-135">In the results panel, select **Heroku**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/heroku-tutorial/tutorial_heroku_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="43c43-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="43c43-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="43c43-138">In this section, you configure and test Azure AD single sign-on with Heroku based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="43c43-138">In this section, you configure and test Azure AD single sign-on with Heroku based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="43c43-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Heroku is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="43c43-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Heroku is to a user in Azure AD.</span></span> <span data-ttu-id="43c43-140">In other words, a link relationship between an Azure AD user and the related user in Heroku needs to be established.</span><span class="sxs-lookup"><span data-stu-id="43c43-140">In other words, a link relationship between an Azure AD user and the related user in Heroku needs to be established.</span></span>

<span data-ttu-id="43c43-141">In Heroku, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="43c43-141">In Heroku, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="43c43-142">To configure and test Azure AD single sign-on with Heroku, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="43c43-142">To configure and test Azure AD single sign-on with Heroku, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="43c43-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="43c43-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="43c43-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="43c43-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="43c43-145">**[Creating a Heroku test user](#creating-a-heroku-test-user)** - to have a counterpart of Britta Simon in Heroku that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="43c43-145">**[Creating a Heroku test user](#creating-a-heroku-test-user)** - to have a counterpart of Britta Simon in Heroku that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="43c43-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="43c43-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="43c43-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="43c43-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="43c43-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="43c43-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="43c43-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Heroku application.</span><span class="sxs-lookup"><span data-stu-id="43c43-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Heroku application.</span></span>

<span data-ttu-id="43c43-150">**To configure Azure AD single sign-on with Heroku, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="43c43-150">**To configure Azure AD single sign-on with Heroku, perform the following steps:**</span></span>

1. <span data-ttu-id="43c43-151">In the Azure portal, on the **Heroku** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="43c43-151">In the Azure portal, on the **Heroku** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="43c43-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="43c43-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/heroku-tutorial/tutorial_heroku_samlbase.png)

1. <span data-ttu-id="43c43-155">On the **Heroku Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="43c43-155">On the **Heroku Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/heroku-tutorial/tutorial_heroku_url.png)

    <span data-ttu-id="43c43-157">a.</span><span class="sxs-lookup"><span data-stu-id="43c43-157">a.</span></span> <span data-ttu-id="43c43-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="43c43-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>    
    `https://sso.heroku.com/saml/<company-name>/init`

    <span data-ttu-id="43c43-159">b.</span><span class="sxs-lookup"><span data-stu-id="43c43-159">b.</span></span> <span data-ttu-id="43c43-160">In the **Identifier URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="43c43-160">In the **Identifier URL** textbox, type a URL using the following pattern:</span></span>            
    `https://sso.heroku.com/saml/<company-name>`

    > [!NOTE]
    ><span data-ttu-id="43c43-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="43c43-161">These values are not real.</span></span> <span data-ttu-id="43c43-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="43c43-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="43c43-163">You get these values from Heroku team, which is described in later sections of this article.</span><span class="sxs-lookup"><span data-stu-id="43c43-163">You get these values from Heroku team, which is described in later sections of this article.</span></span> 
        
1. <span data-ttu-id="43c43-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="43c43-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/heroku-tutorial/tutorial_heroku_certificate.png) 

1. <span data-ttu-id="43c43-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="43c43-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/heroku-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="43c43-168">To enable SSO in Heroku, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="43c43-168">To enable SSO in Heroku, perform the following steps:</span></span>
   
    <span data-ttu-id="43c43-169">a.</span><span class="sxs-lookup"><span data-stu-id="43c43-169">a.</span></span> <span data-ttu-id="43c43-170">Log in to the Heroku account as an administrator.</span><span class="sxs-lookup"><span data-stu-id="43c43-170">Log in to the Heroku account as an administrator.</span></span>

    <span data-ttu-id="43c43-171">b.</span><span class="sxs-lookup"><span data-stu-id="43c43-171">b.</span></span> <span data-ttu-id="43c43-172">Click the **Settings** tab.</span><span class="sxs-lookup"><span data-stu-id="43c43-172">Click the **Settings** tab.</span></span>

    <span data-ttu-id="43c43-173">c.</span><span class="sxs-lookup"><span data-stu-id="43c43-173">c.</span></span> <span data-ttu-id="43c43-174">On the **Single Sign On Page**, click **Upload Metadata**.</span><span class="sxs-lookup"><span data-stu-id="43c43-174">On the **Single Sign On Page**, click **Upload Metadata**.</span></span>

    <span data-ttu-id="43c43-175">d.</span><span class="sxs-lookup"><span data-stu-id="43c43-175">d.</span></span> <span data-ttu-id="43c43-176">Upload the metadata file, which you have downloaded from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="43c43-176">Upload the metadata file, which you have downloaded from the Azure portal.</span></span>

    <span data-ttu-id="43c43-177">e.</span><span class="sxs-lookup"><span data-stu-id="43c43-177">e.</span></span> <span data-ttu-id="43c43-178">When the setup is successful, administrators see a confirmation dialog and the URL of the SSO Login for end users is displayed.</span><span class="sxs-lookup"><span data-stu-id="43c43-178">When the setup is successful, administrators see a confirmation dialog and the URL of the SSO Login for end users is displayed.</span></span> 

    <span data-ttu-id="43c43-179">f.</span><span class="sxs-lookup"><span data-stu-id="43c43-179">f.</span></span> <span data-ttu-id="43c43-180">Copy the **Heroku Login URL** and **Heroku Entity ID** values and go back to **Heroku Domain and URLs** section in Azure portal and paste these values into the **Sign-On Url** and **Identifier** textboxes respectively.</span><span class="sxs-lookup"><span data-stu-id="43c43-180">Copy the **Heroku Login URL** and **Heroku Entity ID** values and go back to **Heroku Domain and URLs** section in Azure portal and paste these values into the **Sign-On Url** and **Identifier** textboxes respectively.</span></span>

    ![Configure Single Sign-On](./media/heroku-tutorial/tutorial_heroku_52.png) 
    
1. <span data-ttu-id="43c43-182">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="43c43-182">Click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="43c43-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="43c43-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="43c43-184">After adding this app from the **Active Directory Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="43c43-184">After adding this app from the **Active Directory Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="43c43-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="43c43-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="43c43-186">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="43c43-186">Creating an Azure AD test user</span></span>

<span data-ttu-id="43c43-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="43c43-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="43c43-189">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="43c43-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="43c43-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="43c43-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/heroku-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="43c43-192">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="43c43-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/heroku-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="43c43-194">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="43c43-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/heroku-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="43c43-196">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="43c43-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/heroku-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="43c43-198">a.</span><span class="sxs-lookup"><span data-stu-id="43c43-198">a.</span></span> <span data-ttu-id="43c43-199">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="43c43-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="43c43-200">b.</span><span class="sxs-lookup"><span data-stu-id="43c43-200">b.</span></span> <span data-ttu-id="43c43-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="43c43-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="43c43-202">c.</span><span class="sxs-lookup"><span data-stu-id="43c43-202">c.</span></span> <span data-ttu-id="43c43-203">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="43c43-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="43c43-204">d.</span><span class="sxs-lookup"><span data-stu-id="43c43-204">d.</span></span> <span data-ttu-id="43c43-205">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="43c43-205">Click **Create**.</span></span>
 
### <a name="creating-a-heroku-test-user"></a><span data-ttu-id="43c43-206">Creating a Heroku test user</span><span class="sxs-lookup"><span data-stu-id="43c43-206">Creating a Heroku test user</span></span>

<span data-ttu-id="43c43-207">In this section, you create a user called Britta Simon in Heroku.</span><span class="sxs-lookup"><span data-stu-id="43c43-207">In this section, you create a user called Britta Simon in Heroku.</span></span> <span data-ttu-id="43c43-208">Heroku supports just-in-time provisioning, which is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="43c43-208">Heroku supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="43c43-209">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="43c43-209">There is no action item for you in this section.</span></span> <span data-ttu-id="43c43-210">A new user is created when accessing Heroku if the user doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="43c43-210">A new user is created when accessing Heroku if the user doesn't exist yet.</span></span> <span data-ttu-id="43c43-211">After the account is provisioned, the end user receives a verification email and needs to click the acknowledgement link.</span><span class="sxs-lookup"><span data-stu-id="43c43-211">After the account is provisioned, the end user receives a verification email and needs to click the acknowledgement link.</span></span>

>[!NOTE]
><span data-ttu-id="43c43-212">If you need to create a user manually, you need to contact the [Heroku Client support team](https://www.heroku.com/support).</span><span class="sxs-lookup"><span data-stu-id="43c43-212">If you need to create a user manually, you need to contact the [Heroku Client support team](https://www.heroku.com/support).</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="43c43-213">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="43c43-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="43c43-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Heroku.</span><span class="sxs-lookup"><span data-stu-id="43c43-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Heroku.</span></span>

![Assign User][200] 

<span data-ttu-id="43c43-216">**To assign Britta Simon to Heroku, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="43c43-216">**To assign Britta Simon to Heroku, perform the following steps:**</span></span>

1. <span data-ttu-id="43c43-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="43c43-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="43c43-219">In the applications list, select **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="43c43-219">In the applications list, select **Heroku**.</span></span>

    ![Configure Single Sign-On](./media/heroku-tutorial/tutorial_heroku_app.png) 

1. <span data-ttu-id="43c43-221">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="43c43-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="43c43-223">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="43c43-223">Click **Add** button.</span></span> <span data-ttu-id="43c43-224">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="43c43-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="43c43-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="43c43-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="43c43-227">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="43c43-227">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="43c43-228">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="43c43-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="43c43-229">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="43c43-229">Testing single sign-on</span></span>

<span data-ttu-id="43c43-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="43c43-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="43c43-231">When you click the Heroku tile in the Access Panel, you should get automatically signed-on to your Heroku application.</span><span class="sxs-lookup"><span data-stu-id="43c43-231">When you click the Heroku tile in the Access Panel, you should get automatically signed-on to your Heroku application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="43c43-232">Additional resources</span><span class="sxs-lookup"><span data-stu-id="43c43-232">Additional resources</span></span>

* [<span data-ttu-id="43c43-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="43c43-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="43c43-234">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="43c43-234">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/heroku-tutorial/tutorial_general_01.png
[2]: ./media/heroku-tutorial/tutorial_general_02.png
[3]: ./media/heroku-tutorial/tutorial_general_03.png
[4]: ./media/heroku-tutorial/tutorial_general_04.png

[100]: ./media/heroku-tutorial/tutorial_general_100.png

[200]: ./media/heroku-tutorial/tutorial_general_200.png
[201]: ./media/heroku-tutorial/tutorial_general_201.png
[202]: ./media/heroku-tutorial/tutorial_general_202.png
[203]: ./media/heroku-tutorial/tutorial_general_203.png
