---
title: 'Tutorial: Azure Active Directory integration with Bime | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Bime.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: bdcf0729-c880-4c95-b739-0f6345b17dd8
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 966c5dcb6f45590fe1b6a8bb2d8b53c37aeed6b2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867025"
---
# <a name="tutorial-azure-active-directory-integration-with-bime"></a><span data-ttu-id="809df-103">Tutorial: Azure Active Directory integration with Bime</span><span class="sxs-lookup"><span data-stu-id="809df-103">Tutorial: Azure Active Directory integration with Bime</span></span>

<span data-ttu-id="809df-104">In this tutorial, you learn how to integrate Bime with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="809df-104">In this tutorial, you learn how to integrate Bime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="809df-105">Integrating Bime with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="809df-105">Integrating Bime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="809df-106">You can control in Azure AD who has access to Bime</span><span class="sxs-lookup"><span data-stu-id="809df-106">You can control in Azure AD who has access to Bime</span></span>
- <span data-ttu-id="809df-107">You can enable your users to automatically get signed-on to Bime (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="809df-107">You can enable your users to automatically get signed-on to Bime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="809df-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="809df-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="809df-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="809df-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="809df-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="809df-110">Prerequisites</span></span>

<span data-ttu-id="809df-111">To configure Azure AD integration with Bime, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="809df-111">To configure Azure AD integration with Bime, you need the following items:</span></span>

- <span data-ttu-id="809df-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="809df-112">An Azure AD subscription</span></span>
- <span data-ttu-id="809df-113">A Bime single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="809df-113">A Bime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="809df-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="809df-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="809df-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="809df-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="809df-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="809df-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="809df-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="809df-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="809df-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="809df-118">Scenario description</span></span>
<span data-ttu-id="809df-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="809df-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="809df-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="809df-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="809df-121">Adding Bime from the gallery</span><span class="sxs-lookup"><span data-stu-id="809df-121">Adding Bime from the gallery</span></span>
1. <span data-ttu-id="809df-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="809df-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bime-from-the-gallery"></a><span data-ttu-id="809df-123">Adding Bime from the gallery</span><span class="sxs-lookup"><span data-stu-id="809df-123">Adding Bime from the gallery</span></span>
<span data-ttu-id="809df-124">To configure the integration of Bime into Azure AD, you need to add Bime from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="809df-124">To configure the integration of Bime into Azure AD, you need to add Bime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="809df-125">**To add Bime from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="809df-125">**To add Bime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="809df-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="809df-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="809df-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="809df-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="809df-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="809df-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="809df-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="809df-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="809df-133">In the search box, type **Bime**.</span><span class="sxs-lookup"><span data-stu-id="809df-133">In the search box, type **Bime**.</span></span>

    ![Creating an Azure AD test user](./media/bime-tutorial/tutorial_bime_search.png)

1. <span data-ttu-id="809df-135">In the results panel, select **Bime**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="809df-135">In the results panel, select **Bime**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/bime-tutorial/tutorial_bime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="809df-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="809df-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="809df-138">In this section, you configure and test Azure AD single sign-on with Bime based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="809df-138">In this section, you configure and test Azure AD single sign-on with Bime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="809df-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bime is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="809df-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bime is to a user in Azure AD.</span></span> <span data-ttu-id="809df-140">In other words, a link relationship between an Azure AD user and the related user in Bime needs to be established.</span><span class="sxs-lookup"><span data-stu-id="809df-140">In other words, a link relationship between an Azure AD user and the related user in Bime needs to be established.</span></span>

<span data-ttu-id="809df-141">In Bime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="809df-141">In Bime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="809df-142">To configure and test Azure AD single sign-on with Bime, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="809df-142">To configure and test Azure AD single sign-on with Bime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="809df-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="809df-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="809df-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="809df-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="809df-145">**[Creating a Bime test user](#creating-a-bime-test-user)** - to have a counterpart of Britta Simon in Bime that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="809df-145">**[Creating a Bime test user](#creating-a-bime-test-user)** - to have a counterpart of Britta Simon in Bime that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="809df-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="809df-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="809df-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="809df-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="809df-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="809df-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="809df-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bime application.</span><span class="sxs-lookup"><span data-stu-id="809df-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bime application.</span></span>

<span data-ttu-id="809df-150">**To configure Azure AD single sign-on with Bime, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="809df-150">**To configure Azure AD single sign-on with Bime, perform the following steps:**</span></span>

1. <span data-ttu-id="809df-151">In the Azure portal, on the **Bime** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="809df-151">In the Azure portal, on the **Bime** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="809df-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="809df-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/bime-tutorial/tutorial_bime_samlbase.png)

1. <span data-ttu-id="809df-155">On the **Bime Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="809df-155">On the **Bime Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/bime-tutorial/tutorial_bime_url.png)

    <span data-ttu-id="809df-157">a.</span><span class="sxs-lookup"><span data-stu-id="809df-157">a.</span></span> <span data-ttu-id="809df-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="809df-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    <span data-ttu-id="809df-159">b.</span><span class="sxs-lookup"><span data-stu-id="809df-159">b.</span></span> <span data-ttu-id="809df-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="809df-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="809df-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="809df-161">These values are not real.</span></span> <span data-ttu-id="809df-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="809df-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="809df-163">Contact [Bime Client support team](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) to get these values.</span><span class="sxs-lookup"><span data-stu-id="809df-163">Contact [Bime Client support team](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) to get these values.</span></span> 
 
1. <span data-ttu-id="809df-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span><span class="sxs-lookup"><span data-stu-id="809df-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![Configure Single Sign-On](./media/bime-tutorial/tutorial_bime_certificate.png) 

1. <span data-ttu-id="809df-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="809df-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/bime-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="809df-168">On the **Bime Configuration** section, click **Configure Bime** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="809df-168">On the **Bime Configuration** section, click **Configure Bime** to open **Configure sign-on** window.</span></span> <span data-ttu-id="809df-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="809df-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/bime-tutorial/tutorial_bime_configure.png) 

1. <span data-ttu-id="809df-171">In a different web browser window, log into your Bime company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="809df-171">In a different web browser window, log into your Bime company site as an administrator.</span></span>

1. <span data-ttu-id="809df-172">In the toolbar, click **Admin**, and then **Account**.</span><span class="sxs-lookup"><span data-stu-id="809df-172">In the toolbar, click **Admin**, and then **Account**.</span></span>
   
    <span data-ttu-id="809df-173">![Admin](./media/bime-tutorial/ic775558.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="809df-173">![Admin](./media/bime-tutorial/ic775558.png "Admin")</span></span>

1. <span data-ttu-id="809df-174">On the account configuration page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="809df-174">On the account configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="809df-175">![Configure Single Sign-On](./media/bime-tutorial/ic775559.png "Configure Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="809df-175">![Configure Single Sign-On](./media/bime-tutorial/ic775559.png "Configure Single Sign-On")</span></span>
   
    <span data-ttu-id="809df-176">a.</span><span class="sxs-lookup"><span data-stu-id="809df-176">a.</span></span> <span data-ttu-id="809df-177">Select **Enable SAML authentication**.</span><span class="sxs-lookup"><span data-stu-id="809df-177">Select **Enable SAML authentication**.</span></span>

    <span data-ttu-id="809df-178">b.</span><span class="sxs-lookup"><span data-stu-id="809df-178">b.</span></span> <span data-ttu-id="809df-179">In the **Remote Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="809df-179">In the **Remote Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="809df-180">c.</span><span class="sxs-lookup"><span data-stu-id="809df-180">c.</span></span>  <span data-ttu-id="809df-181">Paste the **Thumbprint** value from Azure portal into the **Certificate Fingerprint** textbox.</span><span class="sxs-lookup"><span data-stu-id="809df-181">Paste the **Thumbprint** value from Azure portal into the **Certificate Fingerprint** textbox.</span></span>       
   
    <span data-ttu-id="809df-182">d.</span><span class="sxs-lookup"><span data-stu-id="809df-182">d.</span></span> <span data-ttu-id="809df-183">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="809df-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="809df-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="809df-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="809df-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="809df-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="809df-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="809df-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="809df-187">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="809df-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="809df-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="809df-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="809df-190">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="809df-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="809df-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="809df-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/bime-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="809df-193">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="809df-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/bime-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="809df-195">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="809df-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/bime-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="809df-197">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="809df-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/bime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="809df-199">a.</span><span class="sxs-lookup"><span data-stu-id="809df-199">a.</span></span> <span data-ttu-id="809df-200">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="809df-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="809df-201">b.</span><span class="sxs-lookup"><span data-stu-id="809df-201">b.</span></span> <span data-ttu-id="809df-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="809df-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="809df-203">c.</span><span class="sxs-lookup"><span data-stu-id="809df-203">c.</span></span> <span data-ttu-id="809df-204">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="809df-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="809df-205">d.</span><span class="sxs-lookup"><span data-stu-id="809df-205">d.</span></span> <span data-ttu-id="809df-206">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="809df-206">Click **Create**.</span></span>
 
### <a name="creating-a-bime-test-user"></a><span data-ttu-id="809df-207">Creating a Bime test user</span><span class="sxs-lookup"><span data-stu-id="809df-207">Creating a Bime test user</span></span>

<span data-ttu-id="809df-208">In order to enable Azure AD users to log in to Bime, they must be provisioned into Bime.</span><span class="sxs-lookup"><span data-stu-id="809df-208">In order to enable Azure AD users to log in to Bime, they must be provisioned into Bime.</span></span> <span data-ttu-id="809df-209">In the case of Bime, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="809df-209">In the case of Bime, provisioning is a manual task.</span></span>

<span data-ttu-id="809df-210">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="809df-210">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="809df-211">Log in to your **Bime** tenant.</span><span class="sxs-lookup"><span data-stu-id="809df-211">Log in to your **Bime** tenant.</span></span>

1. <span data-ttu-id="809df-212">In the toolbar, click **Admin**, and then **Users**.</span><span class="sxs-lookup"><span data-stu-id="809df-212">In the toolbar, click **Admin**, and then **Users**.</span></span>
   
    <span data-ttu-id="809df-213">![Admin](./media/bime-tutorial/ic775561.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="809df-213">![Admin](./media/bime-tutorial/ic775561.png "Admin")</span></span>

1. <span data-ttu-id="809df-214">In the **Users List**, click **Add New User** (“+”).</span><span class="sxs-lookup"><span data-stu-id="809df-214">In the **Users List**, click **Add New User** (“+”).</span></span>
   
    <span data-ttu-id="809df-215">![Users](./media/bime-tutorial/ic775562.png "Users")</span><span class="sxs-lookup"><span data-stu-id="809df-215">![Users](./media/bime-tutorial/ic775562.png "Users")</span></span>

1. <span data-ttu-id="809df-216">On the **User Details** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="809df-216">On the **User Details** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="809df-217">![User Details](./media/bime-tutorial/ic775563.png "User Details")</span><span class="sxs-lookup"><span data-stu-id="809df-217">![User Details](./media/bime-tutorial/ic775563.png "User Details")</span></span>
   
    <span data-ttu-id="809df-218">a.</span><span class="sxs-lookup"><span data-stu-id="809df-218">a.</span></span> <span data-ttu-id="809df-219">In the **First name** textbox, enter the first name of user like **Britta**.</span><span class="sxs-lookup"><span data-stu-id="809df-219">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="809df-220">b.</span><span class="sxs-lookup"><span data-stu-id="809df-220">b.</span></span> <span data-ttu-id="809df-221">In the **Last name** textbox, enter the last name of user like **Simon**.</span><span class="sxs-lookup"><span data-stu-id="809df-221">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="809df-222">c.</span><span class="sxs-lookup"><span data-stu-id="809df-222">c.</span></span> <span data-ttu-id="809df-223">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="809df-223">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="809df-224">d.</span><span class="sxs-lookup"><span data-stu-id="809df-224">d.</span></span> <span data-ttu-id="809df-225">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="809df-225">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="809df-226">You can use any other Bime user account creation tools or APIs provided by Bime to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="809df-226">You can use any other Bime user account creation tools or APIs provided by Bime to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="809df-227">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="809df-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="809df-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bime.</span><span class="sxs-lookup"><span data-stu-id="809df-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bime.</span></span>

![Assign User][200] 

<span data-ttu-id="809df-230">**To assign Britta Simon to Bime, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="809df-230">**To assign Britta Simon to Bime, perform the following steps:**</span></span>

1. <span data-ttu-id="809df-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="809df-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="809df-233">In the applications list, select **Bime**.</span><span class="sxs-lookup"><span data-stu-id="809df-233">In the applications list, select **Bime**.</span></span>

    ![Configure Single Sign-On](./media/bime-tutorial/tutorial_bime_app.png) 

1. <span data-ttu-id="809df-235">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="809df-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="809df-237">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="809df-237">Click **Add** button.</span></span> <span data-ttu-id="809df-238">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="809df-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="809df-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="809df-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="809df-241">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="809df-241">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="809df-242">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="809df-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="809df-243">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="809df-243">Testing single sign-on</span></span>

<span data-ttu-id="809df-244">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="809df-244">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="809df-245">When you click the Bime tile in the Access Panel, you should get automatically signed-on to your Bime application.</span><span class="sxs-lookup"><span data-stu-id="809df-245">When you click the Bime tile in the Access Panel, you should get automatically signed-on to your Bime application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="809df-246">Additional resources</span><span class="sxs-lookup"><span data-stu-id="809df-246">Additional resources</span></span>

* [<span data-ttu-id="809df-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="809df-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="809df-248">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="809df-248">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/bime-tutorial/tutorial_general_01.png
[2]: ./media/bime-tutorial/tutorial_general_02.png
[3]: ./media/bime-tutorial/tutorial_general_03.png
[4]: ./media/bime-tutorial/tutorial_general_04.png

[100]: ./media/bime-tutorial/tutorial_general_100.png

[200]: ./media/bime-tutorial/tutorial_general_200.png
[201]: ./media/bime-tutorial/tutorial_general_201.png
[202]: ./media/bime-tutorial/tutorial_general_202.png
[203]: ./media/bime-tutorial/tutorial_general_203.png

