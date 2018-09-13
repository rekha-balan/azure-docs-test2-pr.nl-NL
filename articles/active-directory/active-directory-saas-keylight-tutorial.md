---
title: 'Tutorial: Azure Active Directory integration with Keylight | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Keylight.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: jeedes
ms.openlocfilehash: 69e0fa59bacb711f471b5580a94d4cd2f05b5e39
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549402"
---
# <a name="tutorial-azure-active-directory-integration-with-keylight"></a><span data-ttu-id="df7aa-103">Tutorial: Azure Active Directory integration with Keylight</span><span class="sxs-lookup"><span data-stu-id="df7aa-103">Tutorial: Azure Active Directory integration with Keylight</span></span>
<span data-ttu-id="df7aa-104">In this tutorial, you learn how to integrate Keylight with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="df7aa-104">In this tutorial, you learn how to integrate Keylight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="df7aa-105">Integrating Keylight with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="df7aa-105">Integrating Keylight with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="df7aa-106">You can control in Azure AD who has access to Keylight</span><span class="sxs-lookup"><span data-stu-id="df7aa-106">You can control in Azure AD who has access to Keylight</span></span>
* <span data-ttu-id="df7aa-107">You can enable your users to automatically get signed-on to Keylight single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="df7aa-107">You can enable your users to automatically get signed-on to Keylight single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="df7aa-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="df7aa-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="df7aa-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="df7aa-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df7aa-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="df7aa-110">Prerequisites</span></span>
<span data-ttu-id="df7aa-111">To configure Azure AD integration with Keylight, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="df7aa-111">To configure Azure AD integration with Keylight, you need the following items:</span></span>

* <span data-ttu-id="df7aa-112">An Azure subscription</span><span class="sxs-lookup"><span data-stu-id="df7aa-112">An Azure subscription</span></span>
* <span data-ttu-id="df7aa-113">A Keylight single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="df7aa-113">A Keylight single-sign on enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="df7aa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="df7aa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="df7aa-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="df7aa-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="df7aa-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="df7aa-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="df7aa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="df7aa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="df7aa-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="df7aa-118">Scenario Description</span></span>
<span data-ttu-id="df7aa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="df7aa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="df7aa-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="df7aa-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="df7aa-121">Adding Keylight from the gallery</span><span class="sxs-lookup"><span data-stu-id="df7aa-121">Adding Keylight from the gallery</span></span>
2. <span data-ttu-id="df7aa-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="df7aa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-keylight-from-the-gallery"></a><span data-ttu-id="df7aa-123">Add Keylight from the gallery</span><span class="sxs-lookup"><span data-stu-id="df7aa-123">Add Keylight from the gallery</span></span>
<span data-ttu-id="df7aa-124">To configure the integration of Keylight into Azure AD, you need to add Keylight from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="df7aa-124">To configure the integration of Keylight into Azure AD, you need to add Keylight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="df7aa-125">**To add Keylight from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="df7aa-125">**To add Keylight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="df7aa-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="df7aa-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="df7aa-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="df7aa-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="df7aa-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="df7aa-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="df7aa-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="df7aa-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="df7aa-135">In the search box, type **Keylight**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-135">In the search box, type **Keylight**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/tutorial_keylight_01.png)
7. <span data-ttu-id="df7aa-137">In the results pane, select **Keylight**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="df7aa-137">In the results pane, select **Keylight**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/tutorial_keylight_02.png)

## <a name="configure-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="df7aa-139">Configure and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="df7aa-139">Configure and testing Azure AD single sign-on</span></span>
<span data-ttu-id="df7aa-140">In this section, you configure and test Azure AD single sign-on with Keylight based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="df7aa-140">In this section, you configure and test Azure AD single sign-on with Keylight based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="df7aa-141">To configure and test Azure AD single sign-on with Keylight, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="df7aa-141">To configure and test Azure AD single sign-on with Keylight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="df7aa-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="df7aa-142">**[Configure Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="df7aa-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df7aa-143">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="df7aa-144">**[Create a Keylight test user](#creating-a-keylight-test-user)** - to have a counterpart of Britta Simon in Keylight that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="df7aa-144">**[Create a Keylight test user](#creating-a-keylight-test-user)** - to have a counterpart of Britta Simon in Keylight that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="df7aa-145">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="df7aa-145">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="df7aa-146">**[Test Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="df7aa-146">**[Test Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="df7aa-147">Configure Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="df7aa-147">Configure Azure AD Single Sign-On</span></span>
<span data-ttu-id="df7aa-148">In this section, you enable Azure AD single sign-on in the Azure classic portal and configure single sign-on in your Keylight application.</span><span class="sxs-lookup"><span data-stu-id="df7aa-148">In this section, you enable Azure AD single sign-on in the Azure classic portal and configure single sign-on in your Keylight application.</span></span>

<span data-ttu-id="df7aa-149">**To configure Azure AD single sign-on with Keylight, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="df7aa-149">**To configure Azure AD single sign-on with Keylight, perform the following steps:**</span></span>

1. <span data-ttu-id="df7aa-150">In the Azure classic portal, on the **Keylight** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="df7aa-150">In the Azure classic portal, on the **Keylight** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="df7aa-152">On the **How would you like users to sign on to Keylight** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-152">On the **How would you like users to sign on to Keylight** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/tutorial_keylight_03.png) 
3. <span data-ttu-id="df7aa-154">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="df7aa-154">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/tutorial_keylight_04.png) 

    * <span data-ttu-id="df7aa-156">In the Sign On URL textbox, type the URL used by your users to sign-on to your Keylight application using the following pattern: **“https://\<company name\>.keylightgrc.com/Login.aspx?saml=1”**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-156">In the Sign On URL textbox, type the URL used by your users to sign-on to your Keylight application using the following pattern: **“https://\<company name\>.keylightgrc.com/Login.aspx?saml=1”**.</span></span>

4. <span data-ttu-id="df7aa-157">On the **Configure single sign-on at Keylight** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="df7aa-157">On the **Configure single sign-on at Keylight** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/tutorial_keylight_05.png) 
   
    1. <span data-ttu-id="df7aa-159">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="df7aa-159">Click **Download certificate**, and then save the file on your computer.</span></span>
    2. <span data-ttu-id="df7aa-160">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-160">Click **Next**.</span></span>
5. <span data-ttu-id="df7aa-161">To enable SSO in Keylight, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="df7aa-161">To enable SSO in Keylight, perform the following steps:</span></span>
   
    1. <span data-ttu-id="df7aa-162">Sign-on to your Keylight account as administrator.</span><span class="sxs-lookup"><span data-stu-id="df7aa-162">Sign-on to your Keylight account as administrator.</span></span>
    2. <span data-ttu-id="df7aa-163">In the menu on the top, click **Person**, and select **Keylight Setup**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-163">In the menu on the top, click **Person**, and select **Keylight Setup**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/401.png) 
    3. <span data-ttu-id="df7aa-165">In the treeview on the left, click **SAML**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-165">In the treeview on the left, click **SAML**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/402.png) 
    4. <span data-ttu-id="df7aa-167">On the **SAML Settings** dialog, click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-167">On the **SAML Settings** dialog, click **Edit**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/404.png) 
6. <span data-ttu-id="df7aa-169">On the **Edit SAML Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="df7aa-169">On the **Edit SAML Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/405.png) 
   
    1. <span data-ttu-id="df7aa-171">Set **SAML authentication** to **Active**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-171">Set **SAML authentication** to **Active**.</span></span>
    2. <span data-ttu-id="df7aa-172">In Azure AD classic portal, copy the **SAML SSO URL** value, and then paste it into the **Identity Provider Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="df7aa-172">In Azure AD classic portal, copy the **SAML SSO URL** value, and then paste it into the **Identity Provider Login URL** textbox.</span></span>
    3. <span data-ttu-id="df7aa-173">In Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="df7aa-173">In Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider Logout URL** textbox.</span></span>
    4. <span data-ttu-id="df7aa-174">Click **Choose File** to select your downloaded Keylight certificate, and then click **Open** to upload the certificate.</span><span class="sxs-lookup"><span data-stu-id="df7aa-174">Click **Choose File** to select your downloaded Keylight certificate, and then click **Open** to upload the certificate.</span></span>
    5. <span data-ttu-id="df7aa-175">Set **SAML User Id location** to **NameIdentifier element of the subject statement**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-175">Set **SAML User Id location** to **NameIdentifier element of the subject statement**.</span></span>
    6. <span data-ttu-id="df7aa-176">Provide the \*\*Keylight Service Provider using the following pattern: **https://&lt;Company Name&gt;.keylightgrc.com**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-176">Provide the \*\*Keylight Service Provider using the following pattern: **https://&lt;Company Name&gt;.keylightgrc.com**.</span></span>
    7. <span data-ttu-id="df7aa-177">Set the following:</span><span class="sxs-lookup"><span data-stu-id="df7aa-177">Set the following:</span></span>
     * <span data-ttu-id="df7aa-178">**Auto-provision users** to **Active**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-178">**Auto-provision users** to **Active**.</span></span>
     * <span data-ttu-id="df7aa-179">**Auto-provision account type** to **Full User**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-179">**Auto-provision account type** to **Full User**.</span></span>
     * <span data-ttu-id="df7aa-180">**Auto-provision security role**, select **Standard User with SAML**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-180">**Auto-provision security role**, select **Standard User with SAML**.</span></span>
     * <span data-ttu-id="df7aa-181">**Auto-provision security config**, select **Standard User Configuration**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-181">**Auto-provision security config**, select **Standard User Configuration**.</span></span>
    8. <span data-ttu-id="df7aa-182">Enter the following:</span><span class="sxs-lookup"><span data-stu-id="df7aa-182">Enter the following:</span></span>    
     * <span data-ttu-id="df7aa-183">In the Email attribute textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-183">In the Email attribute textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>
     * <span data-ttu-id="df7aa-184">In the **First name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-184">In the **First name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
     * <span data-ttu-id="df7aa-185">In the **Last name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-185">In the **Last name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>
    9. <span data-ttu-id="df7aa-186">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-186">Click **Save**.</span></span>

7. <span data-ttu-id="df7aa-187">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-187">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
8. <span data-ttu-id="df7aa-189">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-189">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="df7aa-191">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="df7aa-191">Create an Azure AD test user</span></span>
<span data-ttu-id="df7aa-192">In this section, you create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="df7aa-192">In this section, you create a test user in the Azure classic portal called Britta Simon.</span></span>

* <span data-ttu-id="df7aa-193">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-193">In the Users list, select **Britta Simon**.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="df7aa-195">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="df7aa-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="df7aa-196">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-196">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="df7aa-198">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="df7aa-198">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="df7aa-199">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-199">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="df7aa-201">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-201">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="df7aa-203">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="df7aa-203">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/create_aaduser_05.png) 
   
   1. <span data-ttu-id="df7aa-205">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="df7aa-205">As Type Of User, select New user in your organization.</span></span>
   2. <span data-ttu-id="df7aa-206">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-206">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   3. <span data-ttu-id="df7aa-207">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-207">Click **Next**.</span></span>
6. <span data-ttu-id="df7aa-208">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="df7aa-208">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/create_aaduser_06.png) 
   
   1. <span data-ttu-id="df7aa-210">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-210">In the **First Name** textbox, type **Britta**.</span></span>    
   2. <span data-ttu-id="df7aa-211">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-211">In the **Last Name** textbox, type, **Simon**.</span></span>
   3. <span data-ttu-id="df7aa-212">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-212">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   4. <span data-ttu-id="df7aa-213">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-213">In the **Role** list, select **User**.</span></span>
   5. <span data-ttu-id="df7aa-214">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-214">Click **Next**.</span></span>
7. <span data-ttu-id="df7aa-215">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-215">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="df7aa-217">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="df7aa-217">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/create_aaduser_08.png) 
   
    1. <span data-ttu-id="df7aa-219">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-219">Write down the value of the **New Password**.</span></span>
    2. <span data-ttu-id="df7aa-220">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-220">Click **Complete**.</span></span>   

### <a name="create-a-keylight-test-user"></a><span data-ttu-id="df7aa-221">Create a Keylight test user</span><span class="sxs-lookup"><span data-stu-id="df7aa-221">Create a Keylight test user</span></span>
<span data-ttu-id="df7aa-222">In this section, you create a user called Britta Simon in Keylight.</span><span class="sxs-lookup"><span data-stu-id="df7aa-222">In this section, you create a user called Britta Simon in Keylight.</span></span> <span data-ttu-id="df7aa-223">Keylight supports just-in-time provisioning, which is enabled by default.</span><span class="sxs-lookup"><span data-stu-id="df7aa-223">Keylight supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="df7aa-224">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="df7aa-224">There is no action item for you in this section.</span></span> <span data-ttu-id="df7aa-225">A new user is created when accessing Keylight if the user doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="df7aa-225">A new user is created when accessing Keylight if the user doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="df7aa-226">If you need to create a user manually, you need to contact the Keylight support team.</span><span class="sxs-lookup"><span data-stu-id="df7aa-226">If you need to create a user manually, you need to contact the Keylight support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="df7aa-227">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="df7aa-227">Assign the Azure AD test user</span></span>
<span data-ttu-id="df7aa-228">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Keylight.</span><span class="sxs-lookup"><span data-stu-id="df7aa-228">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Keylight.</span></span>

![Assign User][200] 

<span data-ttu-id="df7aa-230">**To assign Britta Simon to Keylight, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="df7aa-230">**To assign Britta Simon to Keylight, perform the following steps:**</span></span>

1. <span data-ttu-id="df7aa-231">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="df7aa-231">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="df7aa-233">In the applications list, select **Keylight**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-233">In the applications list, select **Keylight**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/tutorial_keylight_50.png) 
3. <span data-ttu-id="df7aa-235">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-235">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="df7aa-237">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-237">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="df7aa-238">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="df7aa-238">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="df7aa-240">Test Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="df7aa-240">Test Single Sign-On</span></span>
<span data-ttu-id="df7aa-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="df7aa-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="df7aa-242">When you click the Keylight tile in the Access Panel, you should get automatically signed-on to your Keylight application.</span><span class="sxs-lookup"><span data-stu-id="df7aa-242">When you click the Keylight tile in the Access Panel, you should get automatically signed-on to your Keylight application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="df7aa-243">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="df7aa-243">Additional Resources</span></span>
* [<span data-ttu-id="df7aa-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="df7aa-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="df7aa-245">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="df7aa-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-keylight-tutorial/tutorial_general_205.png





























