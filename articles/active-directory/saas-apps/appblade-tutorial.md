---
title: 'Tutorial: Azure Active Directory integration with AppBlade | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and AppBlade.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 3360d7aa-6518-4f99-88bd-b7f7258183e8
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 66c893a89138d7daf7d8118d8e2b1d8389d40ea4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855778"
---
# <a name="tutorial-azure-active-directory-integration-with-appblade"></a><span data-ttu-id="954cd-103">Tutorial: Azure Active Directory integration with AppBlade</span><span class="sxs-lookup"><span data-stu-id="954cd-103">Tutorial: Azure Active Directory integration with AppBlade</span></span>

<span data-ttu-id="954cd-104">In this tutorial, you learn how to integrate AppBlade with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="954cd-104">In this tutorial, you learn how to integrate AppBlade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="954cd-105">Integrating AppBlade with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="954cd-105">Integrating AppBlade with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="954cd-106">You can control in Azure AD who has access to AppBlade</span><span class="sxs-lookup"><span data-stu-id="954cd-106">You can control in Azure AD who has access to AppBlade</span></span>
- <span data-ttu-id="954cd-107">You can enable your users to automatically get signed-on to AppBlade (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="954cd-107">You can enable your users to automatically get signed-on to AppBlade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="954cd-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="954cd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="954cd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="954cd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="954cd-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="954cd-110">Prerequisites</span></span>

<span data-ttu-id="954cd-111">To configure Azure AD integration with AppBlade, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="954cd-111">To configure Azure AD integration with AppBlade, you need the following items:</span></span>

- <span data-ttu-id="954cd-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="954cd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="954cd-113">An AppBlade single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="954cd-113">An AppBlade single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="954cd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="954cd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="954cd-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="954cd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="954cd-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="954cd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="954cd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="954cd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="954cd-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="954cd-118">Scenario description</span></span>
<span data-ttu-id="954cd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="954cd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="954cd-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="954cd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="954cd-121">Adding AppBlade from the gallery</span><span class="sxs-lookup"><span data-stu-id="954cd-121">Adding AppBlade from the gallery</span></span>
2. <span data-ttu-id="954cd-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="954cd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appblade-from-the-gallery"></a><span data-ttu-id="954cd-123">Adding AppBlade from the gallery</span><span class="sxs-lookup"><span data-stu-id="954cd-123">Adding AppBlade from the gallery</span></span>
<span data-ttu-id="954cd-124">To configure the integration of AppBlade into Azure AD, you need to add AppBlade from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="954cd-124">To configure the integration of AppBlade into Azure AD, you need to add AppBlade from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="954cd-125">**To add AppBlade from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="954cd-125">**To add AppBlade from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="954cd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="954cd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="954cd-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="954cd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="954cd-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="954cd-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="954cd-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="954cd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="954cd-133">In the search box, type **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="954cd-133">In the search box, type **AppBlade**.</span></span>

    ![Creating an Azure AD test user](./media/appblade-tutorial/tutorial_appblade_search.png)

5. <span data-ttu-id="954cd-135">In the results panel, select **AppBlade**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="954cd-135">In the results panel, select **AppBlade**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/appblade-tutorial/tutorial_appblade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="954cd-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="954cd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="954cd-138">In this section, you configure and test Azure AD single sign-on with AppBlade based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="954cd-138">In this section, you configure and test Azure AD single sign-on with AppBlade based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="954cd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AppBlade is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="954cd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AppBlade is to a user in Azure AD.</span></span> <span data-ttu-id="954cd-140">In other words, a link relationship between an Azure AD user and the related user in AppBlade needs to be established.</span><span class="sxs-lookup"><span data-stu-id="954cd-140">In other words, a link relationship between an Azure AD user and the related user in AppBlade needs to be established.</span></span>

<span data-ttu-id="954cd-141">In AppBlade, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="954cd-141">In AppBlade, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="954cd-142">To configure and test Azure AD single sign-on with AppBlade, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="954cd-142">To configure and test Azure AD single sign-on with AppBlade, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="954cd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="954cd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="954cd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="954cd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="954cd-145">**[Creating an AppBlade test user](#creating-an-appblade-test-user)** - to have a counterpart of Britta Simon in AppBlade that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="954cd-145">**[Creating an AppBlade test user](#creating-an-appblade-test-user)** - to have a counterpart of Britta Simon in AppBlade that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="954cd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="954cd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="954cd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="954cd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="954cd-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="954cd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="954cd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AppBlade application.</span><span class="sxs-lookup"><span data-stu-id="954cd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AppBlade application.</span></span>

<span data-ttu-id="954cd-150">**To configure Azure AD single sign-on with AppBlade, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="954cd-150">**To configure Azure AD single sign-on with AppBlade, perform the following steps:**</span></span>

1. <span data-ttu-id="954cd-151">In the Azure portal, on the **AppBlade** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="954cd-151">In the Azure portal, on the **AppBlade** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="954cd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="954cd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/appblade-tutorial/tutorial_appblade_samlbase.png)

3. <span data-ttu-id="954cd-155">On the **AppBlade Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="954cd-155">On the **AppBlade Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/appblade-tutorial/tutorial_appblade_url.png)

    <span data-ttu-id="954cd-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.appblade.com/saml/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="954cd-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.appblade.com/saml/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="954cd-158">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="954cd-158">This value is not real.</span></span> <span data-ttu-id="954cd-159">Update the value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="954cd-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="954cd-160">Contact [AppBlade Client support team](mailto:support@appblade.com) to get the value.</span><span class="sxs-lookup"><span data-stu-id="954cd-160">Contact [AppBlade Client support team](mailto:support@appblade.com) to get the value.</span></span> 
 
4. <span data-ttu-id="954cd-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="954cd-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/appblade-tutorial/tutorial_appblade_certificate.png) 

5. <span data-ttu-id="954cd-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="954cd-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/appblade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="954cd-165">To configure single sign-on on **AppBlade** side, you need to send the downloaded **Metadata XML** to [AppBlade support team](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="954cd-165">To configure single sign-on on **AppBlade** side, you need to send the downloaded **Metadata XML** to [AppBlade support team](mailto:support@appblade.com).</span></span> <span data-ttu-id="954cd-166">Also, please ask them to configure the **SSO Issuer URL** as `https://appblade.com/saml`.</span><span class="sxs-lookup"><span data-stu-id="954cd-166">Also, please ask them to configure the **SSO Issuer URL** as `https://appblade.com/saml`.</span></span> <span data-ttu-id="954cd-167">This setting is required for single sign-on to work.</span><span class="sxs-lookup"><span data-stu-id="954cd-167">This setting is required for single sign-on to work.</span></span>


> [!TIP]
> <span data-ttu-id="954cd-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="954cd-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="954cd-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="954cd-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="954cd-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="954cd-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="954cd-171">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="954cd-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="954cd-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="954cd-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="954cd-174">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="954cd-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="954cd-175">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="954cd-175">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/appblade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="954cd-177">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="954cd-177">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/appblade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="954cd-179">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="954cd-179">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/appblade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="954cd-181">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="954cd-181">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/appblade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="954cd-183">a.</span><span class="sxs-lookup"><span data-stu-id="954cd-183">a.</span></span> <span data-ttu-id="954cd-184">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="954cd-184">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="954cd-185">b.</span><span class="sxs-lookup"><span data-stu-id="954cd-185">b.</span></span> <span data-ttu-id="954cd-186">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="954cd-186">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="954cd-187">c.</span><span class="sxs-lookup"><span data-stu-id="954cd-187">c.</span></span> <span data-ttu-id="954cd-188">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="954cd-188">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="954cd-189">d.</span><span class="sxs-lookup"><span data-stu-id="954cd-189">d.</span></span> <span data-ttu-id="954cd-190">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="954cd-190">Click **Create**.</span></span>
 
### <a name="creating-an-appblade-test-user"></a><span data-ttu-id="954cd-191">Creating an AppBlade test user</span><span class="sxs-lookup"><span data-stu-id="954cd-191">Creating an AppBlade test user</span></span>

<span data-ttu-id="954cd-192">The objective of this section is to create a user called Britta Simon in AppBlade.</span><span class="sxs-lookup"><span data-stu-id="954cd-192">The objective of this section is to create a user called Britta Simon in AppBlade.</span></span> <span data-ttu-id="954cd-193">AppBlade supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="954cd-193">AppBlade supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="954cd-194">**Make sure that your domain name is configured with AppBlade for user provisioning. After that only the just-in-time user provisioning works.**</span><span class="sxs-lookup"><span data-stu-id="954cd-194">**Make sure that your domain name is configured with AppBlade for user provisioning. After that only the just-in-time user provisioning works.**</span></span>

<span data-ttu-id="954cd-195">If the user has an email address ending with the domain configured by AppBlade for your account, then the user will automatically join the account as a member with the permission level you specify, which is one of "Basic" (a basic user who can only install applications), "Team Member" (a user who can upload new app versions and manage projects), or "Administrator" (full admin privileges to the account).</span><span class="sxs-lookup"><span data-stu-id="954cd-195">If the user has an email address ending with the domain configured by AppBlade for your account, then the user will automatically join the account as a member with the permission level you specify, which is one of "Basic" (a basic user who can only install applications), "Team Member" (a user who can upload new app versions and manage projects), or "Administrator" (full admin privileges to the account).</span></span> <span data-ttu-id="954cd-196">Normally one would choose Basic and then promote users manually via an Admin login (AppBlade needs to configure either an email-based admin login in advance or promote a user on behalf of the customer after login).</span><span class="sxs-lookup"><span data-stu-id="954cd-196">Normally one would choose Basic and then promote users manually via an Admin login (AppBlade needs to configure either an email-based admin login in advance or promote a user on behalf of the customer after login).</span></span>

<span data-ttu-id="954cd-197">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="954cd-197">There is no action item for you in this section.</span></span> <span data-ttu-id="954cd-198">A new user is created during an attempt to access AppBlade if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="954cd-198">A new user is created during an attempt to access AppBlade if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="954cd-199">If you need to create a user manually, you need to contact the [AppBlade support team](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="954cd-199">If you need to create a user manually, you need to contact the [AppBlade support team](mailto:support@appblade.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="954cd-200">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="954cd-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="954cd-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AppBlade.</span><span class="sxs-lookup"><span data-stu-id="954cd-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AppBlade.</span></span>

![Assign User][200] 

<span data-ttu-id="954cd-203">**To assign Britta Simon to AppBlade, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="954cd-203">**To assign Britta Simon to AppBlade, perform the following steps:**</span></span>

1. <span data-ttu-id="954cd-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="954cd-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="954cd-206">In the applications list, select **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="954cd-206">In the applications list, select **AppBlade**.</span></span>

    ![Configure Single Sign-On](./media/appblade-tutorial/tutorial_appblade_app.png) 

3. <span data-ttu-id="954cd-208">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="954cd-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="954cd-210">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="954cd-210">Click **Add** button.</span></span> <span data-ttu-id="954cd-211">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="954cd-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="954cd-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="954cd-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="954cd-214">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="954cd-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="954cd-215">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="954cd-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="954cd-216">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="954cd-216">Testing single sign-on</span></span>

<span data-ttu-id="954cd-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="954cd-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="954cd-218">When you click the AppBlade tile in the Access Panel, you should get automatically signed-on to your AppBlade application.</span><span class="sxs-lookup"><span data-stu-id="954cd-218">When you click the AppBlade tile in the Access Panel, you should get automatically signed-on to your AppBlade application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="954cd-219">Additional resources</span><span class="sxs-lookup"><span data-stu-id="954cd-219">Additional resources</span></span>

* [<span data-ttu-id="954cd-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="954cd-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="954cd-221">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="954cd-221">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/appblade-tutorial/tutorial_general_01.png
[2]: ./media/appblade-tutorial/tutorial_general_02.png
[3]: ./media/appblade-tutorial/tutorial_general_03.png
[4]: ./media/appblade-tutorial/tutorial_general_04.png

[100]: ./media/appblade-tutorial/tutorial_general_100.png

[200]: ./media/appblade-tutorial/tutorial_general_200.png
[201]: ./media/appblade-tutorial/tutorial_general_201.png
[202]: ./media/appblade-tutorial/tutorial_general_202.png
[203]: ./media/appblade-tutorial/tutorial_general_203.png

