---
title: 'Tutorial: Azure Active Directory integration with Brightspace by Desire2Learn | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Brightspace by Desire2Learn.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: e2d3065b-1f6c-4c45-af78-0d5da3266999
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 6e1f586350a47b70da1b297b608feb9011363dec
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857337"
---
# <a name="tutorial-azure-active-directory-integration-with-brightspace-by-desire2learn"></a><span data-ttu-id="92b36-103">Tutorial: Azure Active Directory integration with Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="92b36-103">Tutorial: Azure Active Directory integration with Brightspace by Desire2Learn</span></span>

<span data-ttu-id="92b36-104">In this tutorial, you learn how to integrate Brightspace by Desire2Learn with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="92b36-104">In this tutorial, you learn how to integrate Brightspace by Desire2Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="92b36-105">Integrating Brightspace by Desire2Learn with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="92b36-105">Integrating Brightspace by Desire2Learn with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="92b36-106">You can control in Azure AD who has access to Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="92b36-106">You can control in Azure AD who has access to Brightspace by Desire2Learn</span></span>
- <span data-ttu-id="92b36-107">You can enable your users to automatically get signed-on to Brightspace by Desire2Learn (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="92b36-107">You can enable your users to automatically get signed-on to Brightspace by Desire2Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="92b36-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="92b36-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="92b36-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="92b36-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92b36-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="92b36-110">Prerequisites</span></span>

<span data-ttu-id="92b36-111">To configure Azure AD integration with Brightspace by Desire2Learn, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="92b36-111">To configure Azure AD integration with Brightspace by Desire2Learn, you need the following items:</span></span>

- <span data-ttu-id="92b36-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="92b36-112">An Azure AD subscription</span></span>
- <span data-ttu-id="92b36-113">A Brightspace by Desire2Learn single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="92b36-113">A Brightspace by Desire2Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="92b36-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="92b36-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="92b36-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="92b36-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="92b36-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="92b36-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="92b36-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="92b36-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="92b36-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="92b36-118">Scenario description</span></span>
<span data-ttu-id="92b36-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="92b36-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="92b36-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="92b36-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="92b36-121">Adding Brightspace by Desire2Learn from the gallery</span><span class="sxs-lookup"><span data-stu-id="92b36-121">Adding Brightspace by Desire2Learn from the gallery</span></span>
1. <span data-ttu-id="92b36-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="92b36-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-brightspace-by-desire2learn-from-the-gallery"></a><span data-ttu-id="92b36-123">Adding Brightspace by Desire2Learn from the gallery</span><span class="sxs-lookup"><span data-stu-id="92b36-123">Adding Brightspace by Desire2Learn from the gallery</span></span>
<span data-ttu-id="92b36-124">To configure the integration of Brightspace by Desire2Learn into Azure AD, you need to add Brightspace by Desire2Learn from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="92b36-124">To configure the integration of Brightspace by Desire2Learn into Azure AD, you need to add Brightspace by Desire2Learn from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="92b36-125">**To add Brightspace by Desire2Learn from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="92b36-125">**To add Brightspace by Desire2Learn from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="92b36-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="92b36-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="92b36-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="92b36-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="92b36-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="92b36-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="92b36-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="92b36-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="92b36-133">In the search box, type **Brightspace by Desire2Learn**.</span><span class="sxs-lookup"><span data-stu-id="92b36-133">In the search box, type **Brightspace by Desire2Learn**.</span></span>

    ![Creating an Azure AD test user](./media/brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_search.png)

1. <span data-ttu-id="92b36-135">In the results panel, select **Brightspace by Desire2Learn**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="92b36-135">In the results panel, select **Brightspace by Desire2Learn**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="92b36-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="92b36-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="92b36-138">In this section, you configure and test Azure AD single sign-on with Brightspace by Desire2Learn based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="92b36-138">In this section, you configure and test Azure AD single sign-on with Brightspace by Desire2Learn based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="92b36-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Brightspace by Desire2Learn is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92b36-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Brightspace by Desire2Learn is to a user in Azure AD.</span></span> <span data-ttu-id="92b36-140">In other words, a link relationship between an Azure AD user and the related user in Brightspace by Desire2Learn needs to be established.</span><span class="sxs-lookup"><span data-stu-id="92b36-140">In other words, a link relationship between an Azure AD user and the related user in Brightspace by Desire2Learn needs to be established.</span></span>

<span data-ttu-id="92b36-141">In Brightspace by Desire2Learn, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="92b36-141">In Brightspace by Desire2Learn, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="92b36-142">To configure and test Azure AD single sign-on with Brightspace by Desire2Learn, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="92b36-142">To configure and test Azure AD single sign-on with Brightspace by Desire2Learn, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="92b36-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="92b36-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="92b36-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="92b36-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="92b36-145">**[Creating a Brightspace by Desire2Learn test user](#creating-a-brightspace-by-desire2learn-test-user)** - to have a counterpart of Britta Simon in Brightspace by Desire2Learn that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="92b36-145">**[Creating a Brightspace by Desire2Learn test user](#creating-a-brightspace-by-desire2learn-test-user)** - to have a counterpart of Britta Simon in Brightspace by Desire2Learn that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="92b36-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="92b36-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="92b36-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="92b36-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="92b36-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="92b36-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="92b36-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Brightspace by Desire2Learn application.</span><span class="sxs-lookup"><span data-stu-id="92b36-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Brightspace by Desire2Learn application.</span></span>

<span data-ttu-id="92b36-150">**To configure Azure AD single sign-on with Brightspace by Desire2Learn, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="92b36-150">**To configure Azure AD single sign-on with Brightspace by Desire2Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="92b36-151">In the Azure portal, on the **Brightspace by Desire2Learn** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="92b36-151">In the Azure portal, on the **Brightspace by Desire2Learn** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="92b36-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="92b36-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_samlbase.png)

1. <span data-ttu-id="92b36-155">On the **Brightspace by Desire2Learn Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="92b36-155">On the **Brightspace by Desire2Learn Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_url.png)

    <span data-ttu-id="92b36-157">a.</span><span class="sxs-lookup"><span data-stu-id="92b36-157">a.</span></span> <span data-ttu-id="92b36-158">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="92b36-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.tenants.brightspace.com/samlLogin`|
    | `https://<companyname>.desire2learn.com/shibboleth-sp`|

    <span data-ttu-id="92b36-159">b.</span><span class="sxs-lookup"><span data-stu-id="92b36-159">b.</span></span> <span data-ttu-id="92b36-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`</span><span class="sxs-lookup"><span data-stu-id="92b36-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="92b36-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="92b36-161">These values are not real.</span></span> <span data-ttu-id="92b36-162">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="92b36-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="92b36-163">Contact [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="92b36-163">Contact [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/) to get these values.</span></span>
 


1. <span data-ttu-id="92b36-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="92b36-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_certificate.png) 

1. <span data-ttu-id="92b36-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="92b36-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/brightspace-desire2learn-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="92b36-168">To configure single sign-on on **Brightspace by Desire2Learn** side, you need to send the downloaded **Metadata XML** to [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="92b36-168">To configure single sign-on on **Brightspace by Desire2Learn** side, you need to send the downloaded **Metadata XML** to [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="92b36-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="92b36-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="92b36-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="92b36-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="92b36-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="92b36-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="92b36-172">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="92b36-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="92b36-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="92b36-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="92b36-175">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="92b36-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="92b36-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="92b36-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/brightspace-desire2learn-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="92b36-178">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="92b36-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/brightspace-desire2learn-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="92b36-180">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="92b36-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/brightspace-desire2learn-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="92b36-182">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="92b36-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/brightspace-desire2learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="92b36-184">a.</span><span class="sxs-lookup"><span data-stu-id="92b36-184">a.</span></span> <span data-ttu-id="92b36-185">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="92b36-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="92b36-186">b.</span><span class="sxs-lookup"><span data-stu-id="92b36-186">b.</span></span> <span data-ttu-id="92b36-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="92b36-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="92b36-188">c.</span><span class="sxs-lookup"><span data-stu-id="92b36-188">c.</span></span> <span data-ttu-id="92b36-189">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="92b36-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="92b36-190">d.</span><span class="sxs-lookup"><span data-stu-id="92b36-190">d.</span></span> <span data-ttu-id="92b36-191">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="92b36-191">Click **Create**.</span></span>
 
### <a name="creating-a-brightspace-by-desire2learn-test-user"></a><span data-ttu-id="92b36-192">Creating a Brightspace by Desire2Learn test user</span><span class="sxs-lookup"><span data-stu-id="92b36-192">Creating a Brightspace by Desire2Learn test user</span></span>

<span data-ttu-id="92b36-193">In order to enable Azure AD users to log into Brightspace by Desire2Learn, they must be provisioned into Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="92b36-193">In order to enable Azure AD users to log into Brightspace by Desire2Learn, they must be provisioned into Brightspace by Desire2Learn.</span></span>  

<span data-ttu-id="92b36-194">In the case of Brightspace by Desire2Learn, the user accounts need to be created by your [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="92b36-194">In the case of Brightspace by Desire2Learn, the user accounts need to be created by your [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

>[!NOTE]
><span data-ttu-id="92b36-195">You can use any other Brightspace by Desire2Learn user account creation tools or APIs provided by Brightspace by Desire2Learn to provision Azure Active Directory user accounts.</span><span class="sxs-lookup"><span data-stu-id="92b36-195">You can use any other Brightspace by Desire2Learn user account creation tools or APIs provided by Brightspace by Desire2Learn to provision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="92b36-196">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="92b36-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="92b36-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="92b36-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Brightspace by Desire2Learn.</span></span>

![Assign User][200] 

<span data-ttu-id="92b36-199">**To assign Britta Simon to Brightspace by Desire2Learn, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="92b36-199">**To assign Britta Simon to Brightspace by Desire2Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="92b36-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="92b36-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="92b36-202">In the applications list, select **Brightspace by Desire2Learn**.</span><span class="sxs-lookup"><span data-stu-id="92b36-202">In the applications list, select **Brightspace by Desire2Learn**.</span></span>

    ![Configure Single Sign-On](./media/brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_app.png) 

1. <span data-ttu-id="92b36-204">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="92b36-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="92b36-206">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="92b36-206">Click **Add** button.</span></span> <span data-ttu-id="92b36-207">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="92b36-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="92b36-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="92b36-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="92b36-210">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="92b36-210">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="92b36-211">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="92b36-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="92b36-212">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="92b36-212">Testing single sign-on</span></span>

<span data-ttu-id="92b36-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="92b36-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="92b36-214">When you click the Brightspace by Desire2Learn tile in the Access Panel, you should get automatically signed-on to your Brightspace by Desire2Learn application.</span><span class="sxs-lookup"><span data-stu-id="92b36-214">When you click the Brightspace by Desire2Learn tile in the Access Panel, you should get automatically signed-on to your Brightspace by Desire2Learn application.</span></span>
<span data-ttu-id="92b36-215">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="92b36-215">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="92b36-216">Additional resources</span><span class="sxs-lookup"><span data-stu-id="92b36-216">Additional resources</span></span>

* [<span data-ttu-id="92b36-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="92b36-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="92b36-218">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="92b36-218">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/brightspace-desire2learn-tutorial/tutorial_general_01.png
[2]: ./media/brightspace-desire2learn-tutorial/tutorial_general_02.png
[3]: ./media/brightspace-desire2learn-tutorial/tutorial_general_03.png
[4]: ./media/brightspace-desire2learn-tutorial/tutorial_general_04.png

[100]: ./media/brightspace-desire2learn-tutorial/tutorial_general_100.png

[200]: ./media/brightspace-desire2learn-tutorial/tutorial_general_200.png
[201]: ./media/brightspace-desire2learn-tutorial/tutorial_general_201.png
[202]: ./media/brightspace-desire2learn-tutorial/tutorial_general_202.png
[203]: ./media/brightspace-desire2learn-tutorial/tutorial_general_203.png

