---
title: 'Tutorial: Azure Active Directory integration with RightScale | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and RightScale.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 155827d54d1705c646c942eed3ea7a923d89e1c8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671615"
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a><span data-ttu-id="09abc-103">Tutorial: Azure Active Directory integration with RightScale</span><span class="sxs-lookup"><span data-stu-id="09abc-103">Tutorial: Azure Active Directory integration with RightScale</span></span>
<span data-ttu-id="09abc-104">The objective of this tutorial is to show you how to integrate RightScale with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="09abc-104">The objective of this tutorial is to show you how to integrate RightScale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="09abc-105">Integrating RightScale with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="09abc-105">Integrating RightScale with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="09abc-106">You can control in Azure AD who has access to RightScale</span><span class="sxs-lookup"><span data-stu-id="09abc-106">You can control in Azure AD who has access to RightScale</span></span>
* <span data-ttu-id="09abc-107">You can enable your users to automatically get signed-on to RightScale single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="09abc-107">You can enable your users to automatically get signed-on to RightScale single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="09abc-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="09abc-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="09abc-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="09abc-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09abc-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="09abc-110">Prerequisites</span></span>
<span data-ttu-id="09abc-111">To configure Azure AD integration with RightScale, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="09abc-111">To configure Azure AD integration with RightScale, you need the following items:</span></span>

* <span data-ttu-id="09abc-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="09abc-112">An Azure AD subscription</span></span>
* <span data-ttu-id="09abc-113">A RightScale single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="09abc-113">A RightScale single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="09abc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="09abc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>  

<span data-ttu-id="09abc-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="09abc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="09abc-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="09abc-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="09abc-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="09abc-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="09abc-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="09abc-118">Scenario description</span></span>
<span data-ttu-id="09abc-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="09abc-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="09abc-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="09abc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="09abc-121">Adding RightScale from the gallery</span><span class="sxs-lookup"><span data-stu-id="09abc-121">Adding RightScale from the gallery</span></span>
2. <span data-ttu-id="09abc-122">Configuring and testing Azure AD single sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="09abc-122">Configuring and testing Azure AD single sign-on (SSO)</span></span>

## <a name="add-rightscale-from-the-gallery"></a><span data-ttu-id="09abc-123">Add RightScale from the gallery</span><span class="sxs-lookup"><span data-stu-id="09abc-123">Add RightScale from the gallery</span></span>
<span data-ttu-id="09abc-124">To configure the integration of RightScale into Azure AD, you need to add RightScale from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="09abc-124">To configure the integration of RightScale into Azure AD, you need to add RightScale from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="09abc-125">**To add RightScale from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="09abc-125">**To add RightScale from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="09abc-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="09abc-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="09abc-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="09abc-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="09abc-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="09abc-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="09abc-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="09abc-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="09abc-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="09abc-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="09abc-135">In the search box, type **RightScale**.</span><span class="sxs-lookup"><span data-stu-id="09abc-135">In the search box, type **RightScale**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_01.png)

7. <span data-ttu-id="09abc-137">In the results pane, select **RightScale**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="09abc-137">In the results pane, select **RightScale**, and then click **Complete** to add the application.</span></span>
   

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="09abc-138">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="09abc-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="09abc-139">The objective of this section is to show you how to configure and test Azure AD SSO with RightScale based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="09abc-139">The objective of this section is to show you how to configure and test Azure AD SSO with RightScale based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="09abc-140">For SSO to work, Azure AD needs to know what the counterpart user in RightScale to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="09abc-140">For SSO to work, Azure AD needs to know what the counterpart user in RightScale to an user in Azure AD is.</span></span> <span data-ttu-id="09abc-141">In other words, a link relationship between an Azure AD user and the related user in RightScale needs to be established.</span><span class="sxs-lookup"><span data-stu-id="09abc-141">In other words, a link relationship between an Azure AD user and the related user in RightScale needs to be established.</span></span>  

<span data-ttu-id="09abc-142">To configure and test Azure AD single sign-on with RightScale, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="09abc-142">To configure and test Azure AD single sign-on with RightScale, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="09abc-143">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="09abc-143">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="09abc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="09abc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="09abc-145">**[Creating a RightScale test user](#creating-a-rightscale-test-user)** - to have a counterpart of Britta Simon in RightScale that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="09abc-145">**[Creating a RightScale test user](#creating-a-rightscale-test-user)** - to have a counterpart of Britta Simon in RightScale that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="09abc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="09abc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="09abc-147">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="09abc-147">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="09abc-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="09abc-148">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="09abc-149">The objective of this section is to enable Azure AD SSO in the classic portal and to configure SSO in your RightScale application.</span><span class="sxs-lookup"><span data-stu-id="09abc-149">The objective of this section is to enable Azure AD SSO in the classic portal and to configure SSO in your RightScale application.</span></span>

<span data-ttu-id="09abc-150">**To configure Azure AD single sign-on with RightScale, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="09abc-150">**To configure Azure AD single sign-on with RightScale, perform the following steps:**</span></span>

1. <span data-ttu-id="09abc-151">In the classic portal, on the **RightScale** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="09abc-151">In the classic portal, on the **RightScale** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 

2. <span data-ttu-id="09abc-153">On the **How would you like users to sign on to RightScale** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="09abc-153">On the **How would you like users to sign on to RightScale** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_03.png) 

3. <span data-ttu-id="09abc-155">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="09abc-155">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_04.png) 
  1. <span data-ttu-id="09abc-157">In the Reply URL textbox, type the URL in the following pattern: `https://login.rightscale.com/login/saml2/consume`</span><span class="sxs-lookup"><span data-stu-id="09abc-157">In the Reply URL textbox, type the URL in the following pattern: `https://login.rightscale.com/login/saml2/consume`</span></span>
  2. <span data-ttu-id="09abc-158">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="09abc-158">Click **Next**.</span></span>

1. <span data-ttu-id="09abc-159">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="09abc-159">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_06.png) 
  1. <span data-ttu-id="09abc-161">In the Sign On URL textbox, type the URL used by your users to sign-on to your RightScale application using the following pattern: `https://login.rightscale.com/`</span><span class="sxs-lookup"><span data-stu-id="09abc-161">In the Sign On URL textbox, type the URL used by your users to sign-on to your RightScale application using the following pattern: `https://login.rightscale.com/`</span></span>
  2. <span data-ttu-id="09abc-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="09abc-162">Click **Next**.</span></span>

2. <span data-ttu-id="09abc-163">On the **Configure single sign-on at RightScale** page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="09abc-163">On the **Configure single sign-on at RightScale** page, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_05.png) 
  1. <span data-ttu-id="09abc-165">Click **Download certificate**, and then save the base-64 encoded certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="09abc-165">Click **Download certificate**, and then save the base-64 encoded certificate file on your computer.</span></span>
  2. <span data-ttu-id="09abc-166">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="09abc-166">Click **Next**.</span></span>

3. <span data-ttu-id="09abc-167">To get SSO configured for your application, you need to sign-on to your RightScale tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="09abc-167">To get SSO configured for your application, you need to sign-on to your RightScale tenant as an administrator.</span></span>
  1. <span data-ttu-id="09abc-168">In the menu on the top, click the **Settings** tab and select **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="09abc-168">In the menu on the top, click the **Settings** tab and select **Single Sign-On**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 
  2. <span data-ttu-id="09abc-170">Click the "**new**" button to add **Your SAML Identity Providers**.</span><span class="sxs-lookup"><span data-stu-id="09abc-170">Click the "**new**" button to add **Your SAML Identity Providers**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png)  
  3. <span data-ttu-id="09abc-172">In the textbox of **Display Name**, input your company name.</span><span class="sxs-lookup"><span data-stu-id="09abc-172">In the textbox of **Display Name**, input your company name.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png) 
  4. <span data-ttu-id="09abc-174">Select **Allow RightScale-initiated SSO using a discovery hint** and input your **domain name** in the below textbox.</span><span class="sxs-lookup"><span data-stu-id="09abc-174">Select **Allow RightScale-initiated SSO using a discovery hint** and input your **domain name** in the below textbox.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)
  5. <span data-ttu-id="09abc-176">Copy SAML SSO URL from Azure AD to **SAML SSO Endpoint** in RightScale.</span><span class="sxs-lookup"><span data-stu-id="09abc-176">Copy SAML SSO URL from Azure AD to **SAML SSO Endpoint** in RightScale.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_005.png)
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)
  6. <span data-ttu-id="09abc-179">Copy Entity ID from Azure AD to **SAML EntityID** in RightScale.</span><span class="sxs-lookup"><span data-stu-id="09abc-179">Copy Entity ID from Azure AD to **SAML EntityID** in RightScale.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_007.png)
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)
  7. <span data-ttu-id="09abc-182">Click **Browser** button to upload the certificate which you downloaded in step4.</span><span class="sxs-lookup"><span data-stu-id="09abc-182">Click **Browser** button to upload the certificate which you downloaded in step4.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)
  8. <span data-ttu-id="09abc-184">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="09abc-184">Click **Save**.</span></span>

4. <span data-ttu-id="09abc-185">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="09abc-185">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]

5. <span data-ttu-id="09abc-187">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="09abc-187">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="09abc-189">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="09abc-189">Create an Azure AD test user</span></span>
<span data-ttu-id="09abc-190">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="09abc-190">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="09abc-192">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="09abc-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="09abc-193">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="09abc-193">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="09abc-195">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="09abc-195">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="09abc-196">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="09abc-196">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="09abc-198">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="09abc-198">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="09abc-200">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="09abc-200">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="09abc-202">As **Type Of User**, select **New user in your organization**.</span><span class="sxs-lookup"><span data-stu-id="09abc-202">As **Type Of User**, select **New user in your organization**.</span></span>
  2. <span data-ttu-id="09abc-203">In the User **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="09abc-203">In the User **Name** textbox, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="09abc-204">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="09abc-204">Click **Next**.</span></span>

6. <span data-ttu-id="09abc-205">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="09abc-205">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="09abc-207">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="09abc-207">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="09abc-208">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="09abc-208">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="09abc-209">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="09abc-209">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="09abc-210">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="09abc-210">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="09abc-211">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="09abc-211">Click **Next**.</span></span>

7. <span data-ttu-id="09abc-212">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="09abc-212">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="09abc-214">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="09abc-214">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/create_aaduser_08.png)  
  1. <span data-ttu-id="09abc-216">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="09abc-216">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="09abc-217">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="09abc-217">Click **Complete**.</span></span>   

### <a name="create-a-rightscale-test-user"></a><span data-ttu-id="09abc-218">Create a RightScale test user</span><span class="sxs-lookup"><span data-stu-id="09abc-218">Create a RightScale test user</span></span>
<span data-ttu-id="09abc-219">In this section, you create a user called Britta Simon in RightScale.</span><span class="sxs-lookup"><span data-stu-id="09abc-219">In this section, you create a user called Britta Simon in RightScale.</span></span> <span data-ttu-id="09abc-220">Please work with RightScale support team via support@rightscale.com to add the users in the RightScale platform.</span><span class="sxs-lookup"><span data-stu-id="09abc-220">Please work with RightScale support team via support@rightscale.com to add the users in the RightScale platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="09abc-221">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="09abc-221">Assign the Azure AD test user</span></span>
<span data-ttu-id="09abc-222">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to RightScale.</span><span class="sxs-lookup"><span data-stu-id="09abc-222">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to RightScale.</span></span>

![Assign User][200] 

<span data-ttu-id="09abc-224">**To assign Britta Simon to RightScale, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="09abc-224">**To assign Britta Simon to RightScale, perform the following steps:**</span></span>

1. <span data-ttu-id="09abc-225">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="09abc-225">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 

2. <span data-ttu-id="09abc-227">In the applications list, select **RightScale**.</span><span class="sxs-lookup"><span data-stu-id="09abc-227">In the applications list, select **RightScale**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_50.png) 

3. <span data-ttu-id="09abc-229">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="09abc-229">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 

4. <span data-ttu-id="09abc-231">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="09abc-231">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="09abc-232">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="09abc-232">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="09abc-234">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="09abc-234">Test single sign-on</span></span>
<span data-ttu-id="09abc-235">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="09abc-235">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="09abc-236">When you click the RightScale tile in the Access Panel, you should get automatically signed-on to your RightScale application.</span><span class="sxs-lookup"><span data-stu-id="09abc-236">When you click the RightScale tile in the Access Panel, you should get automatically signed-on to your RightScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="09abc-237">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="09abc-237">Additional Resources</span></span>
* [<span data-ttu-id="09abc-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09abc-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="09abc-239">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="09abc-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-rightscale-tutorial/tutorial_general_205.png


































