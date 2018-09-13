---
title: 'Tutorial: Azure Active Directory integration with UserEcho | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and UserEcho.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: bedd916b-8f69-4b50-9b8d-56f4ee3bd3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: 0fb87ad1495e64afc1a5b43adb4d07b36732c08e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661882"
---
# <a name="tutorial-azure-active-directory-integration-with-userecho"></a><span data-ttu-id="298b8-103">Tutorial: Azure Active Directory integration with UserEcho</span><span class="sxs-lookup"><span data-stu-id="298b8-103">Tutorial: Azure Active Directory integration with UserEcho</span></span>
<span data-ttu-id="298b8-104">The objective of this tutorial is to show you how to integrate UserEcho with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="298b8-104">The objective of this tutorial is to show you how to integrate UserEcho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="298b8-105">Integrating UserEcho with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="298b8-105">Integrating UserEcho with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="298b8-106">You can control in Azure AD who has access to UserEcho</span><span class="sxs-lookup"><span data-stu-id="298b8-106">You can control in Azure AD who has access to UserEcho</span></span> 
* <span data-ttu-id="298b8-107">You can enable your users to automatically get signed-on to UserEcho single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="298b8-107">You can enable your users to automatically get signed-on to UserEcho single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="298b8-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="298b8-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="298b8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="298b8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="298b8-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="298b8-110">Prerequisites</span></span>
<span data-ttu-id="298b8-111">To configure Azure AD integration with UserEcho, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="298b8-111">To configure Azure AD integration with UserEcho, you need the following items:</span></span>

* <span data-ttu-id="298b8-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="298b8-112">An Azure AD subscription</span></span>
* <span data-ttu-id="298b8-113">A UserEcho SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="298b8-113">A UserEcho SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="298b8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="298b8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="298b8-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="298b8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="298b8-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="298b8-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="298b8-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="298b8-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="298b8-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="298b8-118">Scenario Description</span></span>
<span data-ttu-id="298b8-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="298b8-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>  

<span data-ttu-id="298b8-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="298b8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="298b8-121">Adding UserEcho from the gallery</span><span class="sxs-lookup"><span data-stu-id="298b8-121">Adding UserEcho from the gallery</span></span> 
2. <span data-ttu-id="298b8-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="298b8-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-userecho-from-the-gallery"></a><span data-ttu-id="298b8-123">Add UserEcho from the gallery</span><span class="sxs-lookup"><span data-stu-id="298b8-123">Add UserEcho from the gallery</span></span>
<span data-ttu-id="298b8-124">To configure the integration of UserEcho into Azure AD, you need to add UserEcho from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="298b8-124">To configure the integration of UserEcho into Azure AD, you need to add UserEcho from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="298b8-125">**To add UserEcho from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="298b8-125">**To add UserEcho from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="298b8-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="298b8-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="298b8-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="298b8-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="298b8-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="298b8-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="298b8-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="298b8-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="298b8-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="298b8-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="298b8-135">In the search box, type **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="298b8-135">In the search box, type **UserEcho**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_userecho_01.png)
7. <span data-ttu-id="298b8-137">In the results pane, select **UserEcho**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="298b8-137">In the results pane, select **UserEcho**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_userecho_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="298b8-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="298b8-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="298b8-140">The objective of this section is to show you how to configure and test Azure AD SSO with UserEcho based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="298b8-140">The objective of this section is to show you how to configure and test Azure AD SSO with UserEcho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="298b8-141">For SSO to work, Azure AD needs to know what the counterpart user in UserEcho to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="298b8-141">For SSO to work, Azure AD needs to know what the counterpart user in UserEcho to an user in Azure AD is.</span></span> <span data-ttu-id="298b8-142">In other words, a link relationship between an Azure AD user and the related user in UserEcho needs to be established.</span><span class="sxs-lookup"><span data-stu-id="298b8-142">In other words, a link relationship between an Azure AD user and the related user in UserEcho needs to be established.</span></span>  

<span data-ttu-id="298b8-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in UserEcho.</span><span class="sxs-lookup"><span data-stu-id="298b8-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in UserEcho.</span></span>

<span data-ttu-id="298b8-144">To configure and test Azure AD SSO with UserEcho, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="298b8-144">To configure and test Azure AD SSO with UserEcho, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="298b8-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="298b8-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="298b8-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="298b8-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="298b8-147">**[Creating a UserEcho test user](#creating-a-userecho-test-user)** - to have a counterpart of Britta Simon in UserEcho that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="298b8-147">**[Creating a UserEcho test user](#creating-a-userecho-test-user)** - to have a counterpart of Britta Simon in UserEcho that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="298b8-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="298b8-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="298b8-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="298b8-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="298b8-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="298b8-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="298b8-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your UserEcho application.</span><span class="sxs-lookup"><span data-stu-id="298b8-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your UserEcho application.</span></span> 

<span data-ttu-id="298b8-152">**To configure Azure AD single sign-on with UserEcho, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="298b8-152">**To configure Azure AD single sign-on with UserEcho, perform the following steps:**</span></span>

1. <span data-ttu-id="298b8-153">In the Azure classic portal, on the **UserEcho** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="298b8-153">In the Azure classic portal, on the **UserEcho** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="298b8-155">On the **How would you like users to sign on to UserEcho** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="298b8-155">On the **How would you like users to sign on to UserEcho** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_userecho_03.png) 
3. <span data-ttu-id="298b8-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="298b8-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_userecho_04.png) 
  1. <span data-ttu-id="298b8-159">In the **Sign On URL** textbox, type the URL used by your users to sign on to your UserEcho application (e.g.: *https://fabrikam.UserEcho.com/*).</span><span class="sxs-lookup"><span data-stu-id="298b8-159">In the **Sign On URL** textbox, type the URL used by your users to sign on to your UserEcho application (e.g.: *https://fabrikam.UserEcho.com/*).</span></span>
  2. <span data-ttu-id="298b8-160">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="298b8-160">Click **Next**.</span></span>
4. <span data-ttu-id="298b8-161">On the **Configure single sign-on at UserEcho** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="298b8-161">On the **Configure single sign-on at UserEcho** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_userecho_05.png) 
  1. <span data-ttu-id="298b8-163">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="298b8-163">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="298b8-164">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="298b8-164">Click **Next**.</span></span>
5. <span data-ttu-id="298b8-165">In another browser window, sign on to your UserEcho company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="298b8-165">In another browser window, sign on to your UserEcho company site as an administrator.</span></span>
6. <span data-ttu-id="298b8-166">In the toolbar on the top, click your user name to expand the menu, and then click **Setup**.</span><span class="sxs-lookup"><span data-stu-id="298b8-166">In the toolbar on the top, click your user name to expand the menu, and then click **Setup**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png) 
7. <span data-ttu-id="298b8-168">Click **Integrations**.</span><span class="sxs-lookup"><span data-stu-id="298b8-168">Click **Integrations**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_userecho_07.png) 
8. <span data-ttu-id="298b8-170">Click **Website**, and then click **Single sign-on (SAML2)**.</span><span class="sxs-lookup"><span data-stu-id="298b8-170">Click **Website**, and then click **Single sign-on (SAML2)**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_userecho_08.png) 
9. <span data-ttu-id="298b8-172">On the **Single sign-on (SAML)** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="298b8-172">On the **Single sign-on (SAML)** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_userecho_09.png) 
  1. <span data-ttu-id="298b8-174">As **SAML-enabled**, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="298b8-174">As **SAML-enabled**, select **Yes**.</span></span> 
  2. <span data-ttu-id="298b8-175">In the Azure classic portal, on the Configure single sign-on at UserEcho dialog page, copy the **Single Sign-On Service URL** value, and then paste it in **SAML SSO URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="298b8-175">In the Azure classic portal, on the Configure single sign-on at UserEcho dialog page, copy the **Single Sign-On Service URL** value, and then paste it in **SAML SSO URL** textbox.</span></span>
  3. <span data-ttu-id="298b8-176">In the Azure classic portal, on the Configure single sign-on at UserEcho dialog page, copy the **Remote Logout URL** value, and then paste it into the **Remote logoout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="298b8-176">In the Azure classic portal, on the Configure single sign-on at UserEcho dialog page, copy the **Remote Logout URL** value, and then paste it into the **Remote logoout URL** textbox.</span></span> 
  4. <span data-ttu-id="298b8-177">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="298b8-177">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **X.509 Certificate** textbox.</span></span>    
  5. <span data-ttu-id="298b8-178">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="298b8-178">Click **Save**.</span></span>
10. <span data-ttu-id="298b8-179">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="298b8-179">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
    
     ![Azure AD Single Sign-On][10]
11. <span data-ttu-id="298b8-181">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="298b8-181">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
     ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="298b8-183">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="298b8-183">Create an Azure AD test user</span></span>
<span data-ttu-id="298b8-184">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="298b8-184">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="298b8-186">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="298b8-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="298b8-187">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="298b8-187">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/create_aaduser_09.png)  
2. <span data-ttu-id="298b8-189">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="298b8-189">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="298b8-190">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="298b8-190">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="298b8-192">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="298b8-192">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="298b8-194">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="298b8-194">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/create_aaduser_05.png)  
  1. <span data-ttu-id="298b8-196">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="298b8-196">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="298b8-197">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="298b8-197">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="298b8-198">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="298b8-198">Click **Next**.</span></span>
6. <span data-ttu-id="298b8-199">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="298b8-199">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="298b8-201">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="298b8-201">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="298b8-202">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="298b8-202">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="298b8-203">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="298b8-203">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="298b8-204">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="298b8-204">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="298b8-205">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="298b8-205">Click **Next**.</span></span>
7. <span data-ttu-id="298b8-206">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="298b8-206">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="298b8-208">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="298b8-208">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="298b8-210">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="298b8-210">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="298b8-211">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="298b8-211">Click **Complete**.</span></span>   

### <a name="create-a-userecho-test-user"></a><span data-ttu-id="298b8-212">Create a UserEcho test user</span><span class="sxs-lookup"><span data-stu-id="298b8-212">Create a UserEcho test user</span></span>
<span data-ttu-id="298b8-213">The objective of this section is to create a user called Britta Simon in UserEcho.</span><span class="sxs-lookup"><span data-stu-id="298b8-213">The objective of this section is to create a user called Britta Simon in UserEcho.</span></span>

<span data-ttu-id="298b8-214">**To create a user called Britta Simon in UserEcho, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="298b8-214">**To create a user called Britta Simon in UserEcho, perform the following steps:**</span></span>

1. <span data-ttu-id="298b8-215">Sign-on to your UserEcho company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="298b8-215">Sign-on to your UserEcho company site as an administrator.</span></span>
2. <span data-ttu-id="298b8-216">In the toolbar on the top, click your user name to expand the menu, and then click **Setup**.</span><span class="sxs-lookup"><span data-stu-id="298b8-216">In the toolbar on the top, click your user name to expand the menu, and then click **Setup**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_userecho_06.png) 
3. <span data-ttu-id="298b8-218">Click **Users**, to expand the **Users** section.</span><span class="sxs-lookup"><span data-stu-id="298b8-218">Click **Users**, to expand the **Users** section.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_userecho_10.png) 
4. <span data-ttu-id="298b8-220">Click **Users**.</span><span class="sxs-lookup"><span data-stu-id="298b8-220">Click **Users**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_userecho_11.png) 
5. <span data-ttu-id="298b8-222">Click **Invite a new user**.</span><span class="sxs-lookup"><span data-stu-id="298b8-222">Click **Invite a new user**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_userecho_12.png)
6. <span data-ttu-id="298b8-224">On the **Invite a new user** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="298b8-224">On the **Invite a new user** dialog, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_userecho_13.png) 
  1. <span data-ttu-id="298b8-226">In the **Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="298b8-226">In the **Name** textbox, type **Britta Simon**.</span></span>
  2. <span data-ttu-id="298b8-227">In the **Email** textbox, type Britta's email address in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="298b8-227">In the **Email** textbox, type Britta's email address in the Azure classic portal.</span></span>
  3. <span data-ttu-id="298b8-228">Click **Invite**.</span><span class="sxs-lookup"><span data-stu-id="298b8-228">Click **Invite**.</span></span>

<span data-ttu-id="298b8-229">An invitation is sent to Britta, which enables her to start using UserEcho.</span><span class="sxs-lookup"><span data-stu-id="298b8-229">An invitation is sent to Britta, which enables her to start using UserEcho.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="298b8-230">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="298b8-230">Assign the Azure AD test user</span></span>
<span data-ttu-id="298b8-231">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to UserEcho.</span><span class="sxs-lookup"><span data-stu-id="298b8-231">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to UserEcho.</span></span>

![Assign User][200] 

<span data-ttu-id="298b8-233">**To assign Britta Simon to UserEcho, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="298b8-233">**To assign Britta Simon to UserEcho, perform the following steps:**</span></span>

1. <span data-ttu-id="298b8-234">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="298b8-234">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="298b8-236">In the applications list, select **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="298b8-236">In the applications list, select **UserEcho**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_userecho_50.png) 
3. <span data-ttu-id="298b8-238">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="298b8-238">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="298b8-240">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="298b8-240">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="298b8-241">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="298b8-241">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="298b8-243">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="298b8-243">Test single sign-on</span></span>
<span data-ttu-id="298b8-244">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="298b8-244">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="298b8-245">When you click the UserEcho tile in the Access Panel, you should get automatically signed-on to your UserEcho application.</span><span class="sxs-lookup"><span data-stu-id="298b8-245">When you click the UserEcho tile in the Access Panel, you should get automatically signed-on to your UserEcho application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="298b8-246">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="298b8-246">Additional Resources</span></span>
* [<span data-ttu-id="298b8-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="298b8-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="298b8-248">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="298b8-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-userecho-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-userecho-tutorial/tutorial_general_205.png








































