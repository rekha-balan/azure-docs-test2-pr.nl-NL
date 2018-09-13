---
title: 'Tutorial: Azure Active Directory integration with Wikispaces | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Wikispaces.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 665b95aa-f7f5-4406-9e2a-6fc299a1599c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e4112b431aba706ec1bc9b54f429e1fb43159d6c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968575"
---
# <a name="tutorial-azure-active-directory-integration-with-wikispaces"></a><span data-ttu-id="52f00-103">Tutorial: Azure Active Directory integration with Wikispaces</span><span class="sxs-lookup"><span data-stu-id="52f00-103">Tutorial: Azure Active Directory integration with Wikispaces</span></span>

<span data-ttu-id="52f00-104">In this tutorial, you learn how to integrate Wikispaces with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="52f00-104">In this tutorial, you learn how to integrate Wikispaces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="52f00-105">Integrating Wikispaces with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="52f00-105">Integrating Wikispaces with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="52f00-106">You can control in Azure AD who has access to Wikispaces</span><span class="sxs-lookup"><span data-stu-id="52f00-106">You can control in Azure AD who has access to Wikispaces</span></span>
- <span data-ttu-id="52f00-107">You can enable your users to automatically get signed-on to Wikispaces (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="52f00-107">You can enable your users to automatically get signed-on to Wikispaces (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="52f00-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="52f00-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="52f00-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="52f00-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52f00-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="52f00-110">Prerequisites</span></span>

<span data-ttu-id="52f00-111">To configure Azure AD integration with Wikispaces, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="52f00-111">To configure Azure AD integration with Wikispaces, you need the following items:</span></span>

- <span data-ttu-id="52f00-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="52f00-112">An Azure AD subscription</span></span>
- <span data-ttu-id="52f00-113">A Wikispaces single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="52f00-113">A Wikispaces single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="52f00-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="52f00-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="52f00-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="52f00-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="52f00-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="52f00-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="52f00-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="52f00-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="52f00-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="52f00-118">Scenario description</span></span>
<span data-ttu-id="52f00-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="52f00-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="52f00-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="52f00-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="52f00-121">Adding Wikispaces from the gallery</span><span class="sxs-lookup"><span data-stu-id="52f00-121">Adding Wikispaces from the gallery</span></span>
1. <span data-ttu-id="52f00-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="52f00-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wikispaces-from-the-gallery"></a><span data-ttu-id="52f00-123">Adding Wikispaces from the gallery</span><span class="sxs-lookup"><span data-stu-id="52f00-123">Adding Wikispaces from the gallery</span></span>
<span data-ttu-id="52f00-124">To configure the integration of Wikispaces into Azure AD, you need to add Wikispaces from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="52f00-124">To configure the integration of Wikispaces into Azure AD, you need to add Wikispaces from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="52f00-125">**To add Wikispaces from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="52f00-125">**To add Wikispaces from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="52f00-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="52f00-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="52f00-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="52f00-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="52f00-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="52f00-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="52f00-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="52f00-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="52f00-133">In the search box, type **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="52f00-133">In the search box, type **Wikispaces**.</span></span>

    ![Creating an Azure AD test user](./media/wikispaces-tutorial/tutorial_wikispaces_search.png)

1. <span data-ttu-id="52f00-135">In the results panel, select **Wikispaces**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="52f00-135">In the results panel, select **Wikispaces**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/wikispaces-tutorial/tutorial_wikispaces_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="52f00-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="52f00-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="52f00-138">In this section, you configure and test Azure AD single sign-on with Wikispaces based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="52f00-138">In this section, you configure and test Azure AD single sign-on with Wikispaces based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="52f00-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Wikispaces is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52f00-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Wikispaces is to a user in Azure AD.</span></span> <span data-ttu-id="52f00-140">In other words, a link relationship between an Azure AD user and the related user in Wikispaces needs to be established.</span><span class="sxs-lookup"><span data-stu-id="52f00-140">In other words, a link relationship between an Azure AD user and the related user in Wikispaces needs to be established.</span></span>

<span data-ttu-id="52f00-141">In Wikispaces, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="52f00-141">In Wikispaces, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="52f00-142">To configure and test Azure AD single sign-on with Wikispaces, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="52f00-142">To configure and test Azure AD single sign-on with Wikispaces, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="52f00-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="52f00-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="52f00-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52f00-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="52f00-145">**[Creating a Wikispaces test user](#creating-a-wikispaces-test-user)** - to have a counterpart of Britta Simon in Wikispaces that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="52f00-145">**[Creating a Wikispaces test user](#creating-a-wikispaces-test-user)** - to have a counterpart of Britta Simon in Wikispaces that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="52f00-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="52f00-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="52f00-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="52f00-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="52f00-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="52f00-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="52f00-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wikispaces application.</span><span class="sxs-lookup"><span data-stu-id="52f00-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wikispaces application.</span></span>

<span data-ttu-id="52f00-150">**To configure Azure AD single sign-on with Wikispaces, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="52f00-150">**To configure Azure AD single sign-on with Wikispaces, perform the following steps:**</span></span>

1. <span data-ttu-id="52f00-151">In the Azure portal, on the **Wikispaces** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="52f00-151">In the Azure portal, on the **Wikispaces** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="52f00-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="52f00-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/wikispaces-tutorial/tutorial_wikispaces_samlbase.png)

1. <span data-ttu-id="52f00-155">On the **Wikispaces Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="52f00-155">On the **Wikispaces Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/wikispaces-tutorial/tutorial_wikispaces_url.png)

    <span data-ttu-id="52f00-157">a.</span><span class="sxs-lookup"><span data-stu-id="52f00-157">a.</span></span> <span data-ttu-id="52f00-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.wikispaces.net`</span><span class="sxs-lookup"><span data-stu-id="52f00-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.wikispaces.net`</span></span>

    <span data-ttu-id="52f00-159">b.</span><span class="sxs-lookup"><span data-stu-id="52f00-159">b.</span></span> <span data-ttu-id="52f00-160">In the **Identifier** textbox, type a URL using the following pattern: `https://session.wikispaces.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="52f00-160">In the **Identifier** textbox, type a URL using the following pattern: `https://session.wikispaces.net/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="52f00-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="52f00-161">These values are not real.</span></span> <span data-ttu-id="52f00-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="52f00-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="52f00-163">Contact [Wikispaces Client support team](https://www.wikispaces.com/site/help) to get these values.</span><span class="sxs-lookup"><span data-stu-id="52f00-163">Contact [Wikispaces Client support team](https://www.wikispaces.com/site/help) to get these values.</span></span> 

1. <span data-ttu-id="52f00-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="52f00-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/wikispaces-tutorial/tutorial_wikispaces_certificate.png) 

1. <span data-ttu-id="52f00-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="52f00-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/wikispaces-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="52f00-168">To configure single sign-on on **Wikispaces** side, you need to send the downloaded **Metadata XML** to [Wikispaces support team](https://www.wikispaces.com/site/help).</span><span class="sxs-lookup"><span data-stu-id="52f00-168">To configure single sign-on on **Wikispaces** side, you need to send the downloaded **Metadata XML** to [Wikispaces support team](https://www.wikispaces.com/site/help).</span></span> <span data-ttu-id="52f00-169">You will get a notification as soon as the configuration has been completed.</span><span class="sxs-lookup"><span data-stu-id="52f00-169">You will get a notification as soon as the configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="52f00-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="52f00-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="52f00-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="52f00-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="52f00-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="52f00-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="52f00-173">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="52f00-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="52f00-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52f00-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="52f00-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="52f00-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="52f00-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="52f00-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/wikispaces-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="52f00-179">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="52f00-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/wikispaces-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="52f00-181">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="52f00-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/wikispaces-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="52f00-183">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="52f00-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/wikispaces-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="52f00-185">a.</span><span class="sxs-lookup"><span data-stu-id="52f00-185">a.</span></span> <span data-ttu-id="52f00-186">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="52f00-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="52f00-187">b.</span><span class="sxs-lookup"><span data-stu-id="52f00-187">b.</span></span> <span data-ttu-id="52f00-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="52f00-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="52f00-189">c.</span><span class="sxs-lookup"><span data-stu-id="52f00-189">c.</span></span> <span data-ttu-id="52f00-190">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="52f00-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="52f00-191">d.</span><span class="sxs-lookup"><span data-stu-id="52f00-191">d.</span></span> <span data-ttu-id="52f00-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="52f00-192">Click **Create**.</span></span>
 
### <a name="creating-a-wikispaces-test-user"></a><span data-ttu-id="52f00-193">Creating a Wikispaces test user</span><span class="sxs-lookup"><span data-stu-id="52f00-193">Creating a Wikispaces test user</span></span>

<span data-ttu-id="52f00-194">In order to enable Azure AD users to log in to Wikispaces, they must be provisioned into Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="52f00-194">In order to enable Azure AD users to log in to Wikispaces, they must be provisioned into Wikispaces.</span></span> <span data-ttu-id="52f00-195">In the case of Wikispaces, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="52f00-195">In the case of Wikispaces, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="52f00-196">To provision a user accounts, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="52f00-196">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="52f00-197">Log in to your **Wikispaces** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="52f00-197">Log in to your **Wikispaces** company site as an administrator.</span></span>

1. <span data-ttu-id="52f00-198">Go to **Members**.</span><span class="sxs-lookup"><span data-stu-id="52f00-198">Go to **Members**.</span></span>
   
    <span data-ttu-id="52f00-199">![Members](./media/wikispaces-tutorial/ic787193.png "Members")</span><span class="sxs-lookup"><span data-stu-id="52f00-199">![Members](./media/wikispaces-tutorial/ic787193.png "Members")</span></span>

1. <span data-ttu-id="52f00-200">Click the **Invite People**.</span><span class="sxs-lookup"><span data-stu-id="52f00-200">Click the **Invite People**.</span></span>
   
    <span data-ttu-id="52f00-201">![Invite People](./media/wikispaces-tutorial/ic787194.png "Invite People")</span><span class="sxs-lookup"><span data-stu-id="52f00-201">![Invite People](./media/wikispaces-tutorial/ic787194.png "Invite People")</span></span>

1. <span data-ttu-id="52f00-202">In the **Invite People** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="52f00-202">In the **Invite People** section, perform the following steps:</span></span>
   
    <span data-ttu-id="52f00-203">![Invite People](./media/wikispaces-tutorial/ic787208.png "Invite People")</span><span class="sxs-lookup"><span data-stu-id="52f00-203">![Invite People](./media/wikispaces-tutorial/ic787208.png "Invite People")</span></span>
   
    <span data-ttu-id="52f00-204">a.</span><span class="sxs-lookup"><span data-stu-id="52f00-204">a.</span></span> <span data-ttu-id="52f00-205">Type the **Usernames or Email Address** of a valid AAD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="52f00-205">Type the **Usernames or Email Address** of a valid AAD account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="52f00-206">b.</span><span class="sxs-lookup"><span data-stu-id="52f00-206">b.</span></span> <span data-ttu-id="52f00-207">Click **Send**.</span><span class="sxs-lookup"><span data-stu-id="52f00-207">Click **Send**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="52f00-208">The Azure Active Directory account holder receives an email including a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="52f00-208">The Azure Active Directory account holder receives an email including a link to confirm the account before it becomes active.</span></span>
    
> [!NOTE]
> <span data-ttu-id="52f00-209">You can use any other Wikispaces user account creation tools or APIs provided by Wikispaces to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="52f00-209">You can use any other Wikispaces user account creation tools or APIs provided by Wikispaces to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="52f00-210">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="52f00-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="52f00-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="52f00-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wikispaces.</span></span>

![Assign User][200] 

<span data-ttu-id="52f00-213">**To assign Britta Simon to Wikispaces, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="52f00-213">**To assign Britta Simon to Wikispaces, perform the following steps:**</span></span>

1. <span data-ttu-id="52f00-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="52f00-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="52f00-216">In the applications list, select **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="52f00-216">In the applications list, select **Wikispaces**.</span></span>

    ![Configure Single Sign-On](./media/wikispaces-tutorial/tutorial_wikispaces_app.png) 

1. <span data-ttu-id="52f00-218">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="52f00-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="52f00-220">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="52f00-220">Click **Add** button.</span></span> <span data-ttu-id="52f00-221">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="52f00-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="52f00-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="52f00-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="52f00-224">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="52f00-224">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="52f00-225">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="52f00-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="52f00-226">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="52f00-226">Testing single sign-on</span></span>

<span data-ttu-id="52f00-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="52f00-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="52f00-228">When you click the Wikispaces tile in the Access Panel, you should get automatically signed-on to your Wikispaces application.</span><span class="sxs-lookup"><span data-stu-id="52f00-228">When you click the Wikispaces tile in the Access Panel, you should get automatically signed-on to your Wikispaces application.</span></span>
<span data-ttu-id="52f00-229">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="52f00-229">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="52f00-230">Additional resources</span><span class="sxs-lookup"><span data-stu-id="52f00-230">Additional resources</span></span>

* [<span data-ttu-id="52f00-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52f00-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="52f00-232">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="52f00-232">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/wikispaces-tutorial/tutorial_general_01.png
[2]: ./media/wikispaces-tutorial/tutorial_general_02.png
[3]: ./media/wikispaces-tutorial/tutorial_general_03.png
[4]: ./media/wikispaces-tutorial/tutorial_general_04.png

[100]: ./media/wikispaces-tutorial/tutorial_general_100.png

[200]: ./media/wikispaces-tutorial/tutorial_general_200.png
[201]: ./media/wikispaces-tutorial/tutorial_general_201.png
[202]: ./media/wikispaces-tutorial/tutorial_general_202.png
[203]: ./media/wikispaces-tutorial/tutorial_general_203.png

