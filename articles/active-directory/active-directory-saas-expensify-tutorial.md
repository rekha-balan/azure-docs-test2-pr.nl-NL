---
title: 'Tutorial: Azure Active Directory integration with Expensify | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Expensify.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 1e761484-7a2f-4321-91f4-6d5d0b69344e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: 5e73c5d52e47ca37f9851ae1c82cd8ab82d0e2ac
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661534"
---
# <a name="tutorial-azure-active-directory-integration-with-expensify"></a><span data-ttu-id="6f511-103">Tutorial: Azure Active Directory integration with Expensify</span><span class="sxs-lookup"><span data-stu-id="6f511-103">Tutorial: Azure Active Directory integration with Expensify</span></span>
<span data-ttu-id="6f511-104">In this tutorial, you learn how to integrate Expensify with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6f511-104">In this tutorial, you learn how to integrate Expensify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6f511-105">Integrating Expensify with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="6f511-105">Integrating Expensify with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="6f511-106">You can control in Azure AD who has access to Expensify</span><span class="sxs-lookup"><span data-stu-id="6f511-106">You can control in Azure AD who has access to Expensify</span></span>
* <span data-ttu-id="6f511-107">You can enable your users to automatically get signed-on to Expensify single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="6f511-107">You can enable your users to automatically get signed-on to Expensify single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="6f511-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="6f511-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="6f511-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6f511-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f511-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6f511-110">Prerequisites</span></span>
<span data-ttu-id="6f511-111">To configure Azure AD integration with Expensify, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="6f511-111">To configure Azure AD integration with Expensify, you need the following items:</span></span>

* <span data-ttu-id="6f511-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="6f511-112">An Azure AD subscription</span></span>
* <span data-ttu-id="6f511-113">An Expensify SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="6f511-113">An Expensify SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="6f511-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="6f511-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 

<span data-ttu-id="6f511-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="6f511-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="6f511-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="6f511-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="6f511-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6f511-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6f511-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="6f511-118">Scenario Description</span></span>
<span data-ttu-id="6f511-119">In this tutorial, you test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="6f511-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="6f511-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="6f511-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6f511-121">Adding Expensify from the gallery</span><span class="sxs-lookup"><span data-stu-id="6f511-121">Adding Expensify from the gallery</span></span>
2. <span data-ttu-id="6f511-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6f511-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-expensify-from-the-gallery"></a><span data-ttu-id="6f511-123">Adding Expensify from the gallery</span><span class="sxs-lookup"><span data-stu-id="6f511-123">Adding Expensify from the gallery</span></span>
<span data-ttu-id="6f511-124">To configure the integration of Expensify into Azure AD, you need to add Expensify from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="6f511-124">To configure the integration of Expensify into Azure AD, you need to add Expensify from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6f511-125">**To add Expensify from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6f511-125">**To add Expensify from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6f511-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6f511-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="6f511-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="6f511-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="6f511-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="6f511-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="6f511-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="6f511-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="6f511-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="6f511-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="6f511-135">In the search box, type **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="6f511-135">In the search box, type **Expensify**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_expensify_01.png)
7. <span data-ttu-id="6f511-137">In the results pane, select **Expensify**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="6f511-137">In the results pane, select **Expensify**, and then click **Complete** to add the application.</span></span>

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="6f511-138">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="6f511-138">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="6f511-139">In this section, you configure and test Azure AD single sign-on with Expensify based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6f511-139">In this section, you configure and test Azure AD single sign-on with Expensify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6f511-140">For SSO to work, Azure AD needs to know what the counterpart user in Expensify is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6f511-140">For SSO to work, Azure AD needs to know what the counterpart user in Expensify is to a user in Azure AD.</span></span> <span data-ttu-id="6f511-141">In other words, a link relationship between an Azure AD user and the related user in Expensify needs to be established.</span><span class="sxs-lookup"><span data-stu-id="6f511-141">In other words, a link relationship between an Azure AD user and the related user in Expensify needs to be established.</span></span>  

<span data-ttu-id="6f511-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Expensify.</span><span class="sxs-lookup"><span data-stu-id="6f511-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Expensify.</span></span>

<span data-ttu-id="6f511-143">To configure and test Azure AD SSO with Expensify, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="6f511-143">To configure and test Azure AD SSO with Expensify, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6f511-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="6f511-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6f511-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6f511-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6f511-146">**[Creating an Expensify test user](#creating-an-expensify-test-user)** - to have a counterpart of Britta Simon in Expensify that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="6f511-146">**[Creating an Expensify test user](#creating-an-expensify-test-user)** - to have a counterpart of Britta Simon in Expensify that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="6f511-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6f511-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6f511-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="6f511-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="6f511-149">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="6f511-149">Configure Azure AD SSO</span></span>
<span data-ttu-id="6f511-150">In this section, you enable Azure AD SSO in the classic portal and configure single sign-on in your Expensify application.</span><span class="sxs-lookup"><span data-stu-id="6f511-150">In this section, you enable Azure AD SSO in the classic portal and configure single sign-on in your Expensify application.</span></span>

<span data-ttu-id="6f511-151">**To configure Azure AD SSO with Expensify, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6f511-151">**To configure Azure AD SSO with Expensify, perform the following steps:**</span></span>

1. <span data-ttu-id="6f511-152">In the classic portal, on the **Expensify** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="6f511-152">In the classic portal, on the **Expensify** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="6f511-154">On the **How would you like users to sign on to Expensify** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6f511-154">On the **How would you like users to sign on to Expensify** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_expensify_03.png) 
3. <span data-ttu-id="6f511-156">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6f511-156">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_expensify_04.png) 
  1. <span data-ttu-id="6f511-158">In the Sign On URL textbox, type the URL used by your users to sign-on to your Expensify application using the following pattern: **“https://www.expensify.com/authentication/saml/login”**.</span><span class="sxs-lookup"><span data-stu-id="6f511-158">In the Sign On URL textbox, type the URL used by your users to sign-on to your Expensify application using the following pattern: **“https://www.expensify.com/authentication/saml/login”**.</span></span>
4. <span data-ttu-id="6f511-159">On the **Configure single sign-on at Expensify** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6f511-159">On the **Configure single sign-on at Expensify** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_expensify_05.png)   
  1. <span data-ttu-id="6f511-161">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="6f511-161">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="6f511-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6f511-162">Click **Next**.</span></span>
5. <span data-ttu-id="6f511-163">To enable SSO in Expensify you first need to enable **Domain Control** in the application.</span><span class="sxs-lookup"><span data-stu-id="6f511-163">To enable SSO in Expensify you first need to enable **Domain Control** in the application.</span></span> <span data-ttu-id="6f511-164">You can enable Domain Control in the application.</span><span class="sxs-lookup"><span data-stu-id="6f511-164">You can enable Domain Control in the application.</span></span> <span data-ttu-id="6f511-165">The steps are listed [here](http://help.expensify.com/domain-control).</span><span class="sxs-lookup"><span data-stu-id="6f511-165">The steps are listed [here](http://help.expensify.com/domain-control).</span></span> <span data-ttu-id="6f511-166">For additional support, you can contact the Expensify support via [help@expensify.com](mailto:help@expensify.com).</span><span class="sxs-lookup"><span data-stu-id="6f511-166">For additional support, you can contact the Expensify support via [help@expensify.com](mailto:help@expensify.com).</span></span> <span data-ttu-id="6f511-167">Once you have Domain Control enabled, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="6f511-167">Once you have Domain Control enabled, follow these steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_expensify_51.png) 
  1. <span data-ttu-id="6f511-169">Sign on to your Expensify application.</span><span class="sxs-lookup"><span data-stu-id="6f511-169">Sign on to your Expensify application.</span></span>
  2. <span data-ttu-id="6f511-170">In the toolbar on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="6f511-170">In the toolbar on the top, click **Admin**.</span></span>
  3. <span data-ttu-id="6f511-171">In the left panel, click **Domain Control**.</span><span class="sxs-lookup"><span data-stu-id="6f511-171">In the left panel, click **Domain Control**.</span></span>
  4. <span data-ttu-id="6f511-172">Click your verified domain name.</span><span class="sxs-lookup"><span data-stu-id="6f511-172">Click your verified domain name.</span></span>
  5. <span data-ttu-id="6f511-173">In the left panel, click **SAML**, and then select **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="6f511-173">In the left panel, click **SAML**, and then select **Enabled**.</span></span>
  6. <span data-ttu-id="6f511-174">Open the downloaded Federation Metadata from Azure AD, copy the content, and then paste it into the **Identity Provider Metadata** textbox.</span><span class="sxs-lookup"><span data-stu-id="6f511-174">Open the downloaded Federation Metadata from Azure AD, copy the content, and then paste it into the **Identity Provider Metadata** textbox.</span></span>
6. <span data-ttu-id="6f511-175">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6f511-175">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="6f511-177">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="6f511-177">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6f511-179">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6f511-179">Create an Azure AD test user</span></span>
<span data-ttu-id="6f511-180">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6f511-180">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="6f511-182">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6f511-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6f511-183">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6f511-183">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="6f511-185">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="6f511-185">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="6f511-186">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="6f511-186">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="6f511-188">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="6f511-188">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="6f511-190">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6f511-190">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="6f511-192">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="6f511-192">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="6f511-193">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6f511-193">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="6f511-194">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6f511-194">Click **Next**.</span></span>
6. <span data-ttu-id="6f511-195">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6f511-195">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="6f511-197">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="6f511-197">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="6f511-198">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="6f511-198">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="6f511-199">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6f511-199">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="6f511-200">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="6f511-200">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="6f511-201">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6f511-201">Click **Next**.</span></span>
7. <span data-ttu-id="6f511-202">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="6f511-202">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="6f511-204">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6f511-204">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="6f511-206">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="6f511-206">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="6f511-207">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="6f511-207">Click **Complete**.</span></span>   

### <a name="create-an-expensify-test-user"></a><span data-ttu-id="6f511-208">Create an Expensify test user</span><span class="sxs-lookup"><span data-stu-id="6f511-208">Create an Expensify test user</span></span>
<span data-ttu-id="6f511-209">In this section, you create a user called Britta Simon in Expensify.</span><span class="sxs-lookup"><span data-stu-id="6f511-209">In this section, you create a user called Britta Simon in Expensify.</span></span> <span data-ttu-id="6f511-210">Please work with Expensify support team to add the users in the Expensify platform.</span><span class="sxs-lookup"><span data-stu-id="6f511-210">Please work with Expensify support team to add the users in the Expensify platform.</span></span>

>[!NOTE]
><span data-ttu-id="6f511-211">If you need to create a user manually, you need to contact the Expensify support team.</span><span class="sxs-lookup"><span data-stu-id="6f511-211">If you need to create a user manually, you need to contact the Expensify support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6f511-212">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6f511-212">Assign the Azure AD test user</span></span>
<span data-ttu-id="6f511-213">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Expensify.</span><span class="sxs-lookup"><span data-stu-id="6f511-213">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Expensify.</span></span>

![Assign User][200] 

<span data-ttu-id="6f511-215">**To assign Britta Simon to Expensify, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6f511-215">**To assign Britta Simon to Expensify, perform the following steps:**</span></span>

1. <span data-ttu-id="6f511-216">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="6f511-216">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="6f511-218">In the applications list, select **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="6f511-218">In the applications list, select **Expensify**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_expensify_50.png) 
3. <span data-ttu-id="6f511-220">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="6f511-220">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="6f511-222">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6f511-222">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="6f511-223">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="6f511-223">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="6f511-225">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="6f511-225">Test single sign-on</span></span>
<span data-ttu-id="6f511-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="6f511-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="6f511-227">When you click the Expensify tile in the Access Panel, you should get automatically signed-on to your Expensify application.</span><span class="sxs-lookup"><span data-stu-id="6f511-227">When you click the Expensify tile in the Access Panel, you should get automatically signed-on to your Expensify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6f511-228">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="6f511-228">Additional Resources</span></span>
* [<span data-ttu-id="6f511-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6f511-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6f511-230">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6f511-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-expensify-tutorial/tutorial_general_205.png

























