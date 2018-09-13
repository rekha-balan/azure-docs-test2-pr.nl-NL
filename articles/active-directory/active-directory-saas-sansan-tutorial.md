---
title: 'Tutorial: Azure Active Directory integration with SanSan | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SanSan.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: f653a0f2-c44a-4670-b936-68c136b578ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: jeedes
ms.openlocfilehash: 11f0e00ed397dd955ae88040ba074a1590ab6e88
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553886"
---
# <a name="tutorial-azure-active-directory-integration-with-sansan"></a><span data-ttu-id="09cb7-103">Tutorial: Azure Active Directory integration with SanSan</span><span class="sxs-lookup"><span data-stu-id="09cb7-103">Tutorial: Azure Active Directory integration with SanSan</span></span>
<span data-ttu-id="09cb7-104">In this tutorial, you learn how to integrate SanSan with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="09cb7-104">In this tutorial, you learn how to integrate SanSan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="09cb7-105">Integrating SanSan with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="09cb7-105">Integrating SanSan with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="09cb7-106">You can control in Azure AD who has access to SanSan</span><span class="sxs-lookup"><span data-stu-id="09cb7-106">You can control in Azure AD who has access to SanSan</span></span>
* <span data-ttu-id="09cb7-107">You can enable your users to automatically get signed-on to SanSan single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="09cb7-107">You can enable your users to automatically get signed-on to SanSan single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="09cb7-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="09cb7-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="09cb7-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="09cb7-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09cb7-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="09cb7-110">Prerequisites</span></span>
<span data-ttu-id="09cb7-111">To configure Azure AD integration with SanSan, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="09cb7-111">To configure Azure AD integration with SanSan, you need the following items:</span></span>

* <span data-ttu-id="09cb7-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="09cb7-112">An Azure AD subscription</span></span>
* <span data-ttu-id="09cb7-113">A SanSan single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="09cb7-113">A SanSan single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="09cb7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="09cb7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="09cb7-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="09cb7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="09cb7-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="09cb7-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="09cb7-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="09cb7-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="09cb7-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="09cb7-118">Scenario description</span></span>
<span data-ttu-id="09cb7-119">In this tutorial, you test Microsoft Microsoft Azure AD Single Sign-On in a test environment.</span><span class="sxs-lookup"><span data-stu-id="09cb7-119">In this tutorial, you test Microsoft Microsoft Azure AD Single Sign-On in a test environment.</span></span> 

<span data-ttu-id="09cb7-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="09cb7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="09cb7-121">Adding SanSan from the gallery</span><span class="sxs-lookup"><span data-stu-id="09cb7-121">Adding SanSan from the gallery</span></span>
2. <span data-ttu-id="09cb7-122">Configuring and testing Microsoft Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="09cb7-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-sansan-from-the-gallery"></a><span data-ttu-id="09cb7-123">Add SanSan from the gallery</span><span class="sxs-lookup"><span data-stu-id="09cb7-123">Add SanSan from the gallery</span></span>
<span data-ttu-id="09cb7-124">To configure the integration of SanSan into Azure AD, you need to add SanSan from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="09cb7-124">To configure the integration of SanSan into Azure AD, you need to add SanSan from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="09cb7-125">**To add SanSan from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="09cb7-125">**To add SanSan from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="09cb7-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="09cb7-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="09cb7-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="09cb7-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="09cb7-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="09cb7-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="09cb7-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="09cb7-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="09cb7-135">In the search box, type **SanSan**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-135">In the search box, type **SanSan**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/tutorial_sansan_01.png)
7. <span data-ttu-id="09cb7-137">In the results pane, select **SanSan**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="09cb7-137">In the results pane, select **SanSan**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/tutorial_sansan_06.png)

## <a name="configure-and-test-microsoft-azure-ad-single-sign-on"></a><span data-ttu-id="09cb7-139">Configure and test Microsoft Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="09cb7-139">Configure and test Microsoft Azure AD Single Sign-On</span></span>
<span data-ttu-id="09cb7-140">In this section, you configure and test Microsoft Azure AD SSO with SanSan based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="09cb7-140">In this section, you configure and test Microsoft Azure AD SSO with SanSan based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="09cb7-141">For SSO to work, Azure AD needs to know what the counterpart user in SanSan is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="09cb7-141">For SSO to work, Azure AD needs to know what the counterpart user in SanSan is to a user in Azure AD.</span></span> <span data-ttu-id="09cb7-142">In other words, a link relationship between an Azure AD user and the related user in SanSan needs to be established.</span><span class="sxs-lookup"><span data-stu-id="09cb7-142">In other words, a link relationship between an Azure AD user and the related user in SanSan needs to be established.</span></span>

<span data-ttu-id="09cb7-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SanSan.</span><span class="sxs-lookup"><span data-stu-id="09cb7-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SanSan.</span></span>

<span data-ttu-id="09cb7-144">To configure and test Microsoft Azure AD SSO with SanSan, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="09cb7-144">To configure and test Microsoft Azure AD SSO with SanSan, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="09cb7-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="09cb7-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="09cb7-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="09cb7-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="09cb7-147">**[Creating an SanSan test user](#creating-an-sansan-test-user)** - to have a counterpart of Britta Simon in SanSan that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="09cb7-147">**[Creating an SanSan test user](#creating-an-sansan-test-user)** - to have a counterpart of Britta Simon in SanSan that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="09cb7-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="09cb7-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="09cb7-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="09cb7-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-microsoft-azure-ad-sso"></a><span data-ttu-id="09cb7-150">Configure Microsoft Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="09cb7-150">Configure Microsoft Azure AD SSO</span></span>

<span data-ttu-id="09cb7-151">In this section, you enable Microsoft Azure AD Single Sign-On in the classic portal and configure single sign-on in your SanSan application.</span><span class="sxs-lookup"><span data-stu-id="09cb7-151">In this section, you enable Microsoft Azure AD Single Sign-On in the classic portal and configure single sign-on in your SanSan application.</span></span>

<span data-ttu-id="09cb7-152">**To configure Microsoft Azure AD Single Sign-On with SanSan, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="09cb7-152">**To configure Microsoft Azure AD Single Sign-On with SanSan, perform the following steps:**</span></span>

1. <span data-ttu-id="09cb7-153">In the Azure classic portal, on the **SanSan** application integration page, click Configure single sign-on to open the Configure Single Sign-On dialog.</span><span class="sxs-lookup"><span data-stu-id="09cb7-153">In the Azure classic portal, on the **SanSan** application integration page, click Configure single sign-on to open the Configure Single Sign-On dialog.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/tutorial_general_05.png) 
2. <span data-ttu-id="09cb7-155">On the **How would you like users to sign on to SanSan** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-155">On the **How would you like users to sign on to SanSan** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/tutorial_sansan_03.png) 
3. <span data-ttu-id="09cb7-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="09cb7-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/tutorial_sansan_04.png)    
  1. <span data-ttu-id="09cb7-159">In the **Sign On URL** textbox, type the URL in the following pattern:</span><span class="sxs-lookup"><span data-stu-id="09cb7-159">In the **Sign On URL** textbox, type the URL in the following pattern:</span></span>
   
    | <span data-ttu-id="09cb7-160">Environment</span><span class="sxs-lookup"><span data-stu-id="09cb7-160">Environment</span></span> | <span data-ttu-id="09cb7-161">URL</span><span class="sxs-lookup"><span data-stu-id="09cb7-161">URL</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="09cb7-162">PC web</span><span class="sxs-lookup"><span data-stu-id="09cb7-162">PC web</span></span> |`https://ap.sansan.com/v/saml2/<company name>/acs` |
    | <span data-ttu-id="09cb7-163">Native Mobile app</span><span class="sxs-lookup"><span data-stu-id="09cb7-163">Native Mobile app</span></span> |`https://internal.api.sansan.com/saml2/<company name>/acs` |
    | <span data-ttu-id="09cb7-164">Mobile browser settings</span><span class="sxs-lookup"><span data-stu-id="09cb7-164">Mobile browser settings</span></span> |`https://ap.sansan.com/s/saml2/<company name>/acs` 
  2. <span data-ttu-id="09cb7-165">In the **Identifier** textbox type the URL in the following pattern:</span><span class="sxs-lookup"><span data-stu-id="09cb7-165">In the **Identifier** textbox type the URL in the following pattern:</span></span> 

    | <span data-ttu-id="09cb7-166">Environment</span><span class="sxs-lookup"><span data-stu-id="09cb7-166">Environment</span></span>             | <span data-ttu-id="09cb7-167">URL</span><span class="sxs-lookup"><span data-stu-id="09cb7-167">URL</span></span> |
    | :--                     | :-- |
    | <span data-ttu-id="09cb7-168">PC web</span><span class="sxs-lookup"><span data-stu-id="09cb7-168">PC web</span></span>                  | `https://ap.sansan.com/v/saml2/<company name>`|
    | <span data-ttu-id="09cb7-169">Native Mobile app</span><span class="sxs-lookup"><span data-stu-id="09cb7-169">Native Mobile app</span></span>       | `https://internal.api.sansan.com/saml2/<company name>` |
    | <span data-ttu-id="09cb7-170">Mobile browser settings</span><span class="sxs-lookup"><span data-stu-id="09cb7-170">Mobile browser settings</span></span> | `https://ap.sansan.com/s/saml2/<company name>` |
  3. <span data-ttu-id="09cb7-171">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-171">Click **Next**.</span></span>

1. <span data-ttu-id="09cb7-172">On the **Configure single sign-on at SanSan** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="09cb7-172">On the **Configure single sign-on at SanSan** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/tutorial_sansan_05.png) 
  1. <span data-ttu-id="09cb7-174">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="09cb7-174">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="09cb7-175">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-175">Click **Next**.</span></span>
2. <span data-ttu-id="09cb7-176">To get SSO configured for your application, contact SanSan Support team and they will assist to configure SSO.</span><span class="sxs-lookup"><span data-stu-id="09cb7-176">To get SSO configured for your application, contact SanSan Support team and they will assist to configure SSO.</span></span> <span data-ttu-id="09cb7-177">Please provide them with the following information :</span><span class="sxs-lookup"><span data-stu-id="09cb7-177">Please provide them with the following information :</span></span>
   
  * <span data-ttu-id="09cb7-178">The downloaded **certificate**</span><span class="sxs-lookup"><span data-stu-id="09cb7-178">The downloaded **certificate**</span></span>
  * <span data-ttu-id="09cb7-179">The **Identity Provider ID**</span><span class="sxs-lookup"><span data-stu-id="09cb7-179">The **Identity Provider ID**</span></span>   
  * <span data-ttu-id="09cb7-180">The **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="09cb7-180">The **SAML SSO URL**</span></span>
  * <span data-ttu-id="09cb7-181">The **Single Sign Out Service URL**</span><span class="sxs-lookup"><span data-stu-id="09cb7-181">The **Single Sign Out Service URL**</span></span>

>[!NOTE]
><span data-ttu-id="09cb7-182">PC browser setting also work for Mobile app and Mobile browser along with PC web.</span><span class="sxs-lookup"><span data-stu-id="09cb7-182">PC browser setting also work for Mobile app and Mobile browser along with PC web.</span></span>  
> 

1. <span data-ttu-id="09cb7-183">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-183">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
2. <span data-ttu-id="09cb7-185">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-185">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="09cb7-187">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="09cb7-187">Create an Azure AD test user</span></span>
<span data-ttu-id="09cb7-188">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="09cb7-188">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

* <span data-ttu-id="09cb7-189">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-189">In the Users list, select **Britta Simon**.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="09cb7-191">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="09cb7-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="09cb7-192">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-192">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="09cb7-194">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="09cb7-194">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="09cb7-195">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-195">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="09cb7-197">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-197">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="09cb7-199">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="09cb7-199">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/create_aaduser_05.png)  
  1. <span data-ttu-id="09cb7-201">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="09cb7-201">As Type Of User, select New user in your organization.</span></span> 
  2. <span data-ttu-id="09cb7-202">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-202">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="09cb7-203">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-203">Click **Next**.</span></span>
6. <span data-ttu-id="09cb7-204">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="09cb7-204">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="09cb7-206">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-206">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="09cb7-207">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-207">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="09cb7-208">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-208">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="09cb7-209">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-209">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="09cb7-210">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-210">Click **Next**.</span></span>
7. <span data-ttu-id="09cb7-211">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-211">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="09cb7-213">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="09cb7-213">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/create_aaduser_08.png) 
   1. <span data-ttu-id="09cb7-215">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-215">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="09cb7-216">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-216">Click **Complete**.</span></span>   

### <a name="create-an-sansan-test-user"></a><span data-ttu-id="09cb7-217">Create an SanSan test user</span><span class="sxs-lookup"><span data-stu-id="09cb7-217">Create an SanSan test user</span></span>
<span data-ttu-id="09cb7-218">In this section, you create a user called Britta Simon in SanSan.</span><span class="sxs-lookup"><span data-stu-id="09cb7-218">In this section, you create a user called Britta Simon in SanSan.</span></span> <span data-ttu-id="09cb7-219">SanSan application need the user to be provisioned in the application before doing SSO.</span><span class="sxs-lookup"><span data-stu-id="09cb7-219">SanSan application need the user to be provisioned in the application before doing SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="09cb7-220">If you need to create a user manually or batch of users, you need to contact the SanSan support team.</span><span class="sxs-lookup"><span data-stu-id="09cb7-220">If you need to create a user manually or batch of users, you need to contact the SanSan support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="09cb7-221">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="09cb7-221">Assign the Azure AD test user</span></span>
<span data-ttu-id="09cb7-222">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to SanSan.</span><span class="sxs-lookup"><span data-stu-id="09cb7-222">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to SanSan.</span></span>

![Assign User][200] 

<span data-ttu-id="09cb7-224">**To assign Britta Simon to SanSan, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="09cb7-224">**To assign Britta Simon to SanSan, perform the following steps:**</span></span>

1. <span data-ttu-id="09cb7-225">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="09cb7-225">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="09cb7-227">In the applications list, select **SanSan**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-227">In the applications list, select **SanSan**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/tutorial_sansan_50.png) 
3. <span data-ttu-id="09cb7-229">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-229">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="09cb7-231">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-231">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="09cb7-232">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="09cb7-232">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="09cb7-234">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="09cb7-234">Test single sign-on</span></span>
<span data-ttu-id="09cb7-235">In this section, you test your Microsoft Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="09cb7-235">In this section, you test your Microsoft Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="09cb7-236">When you click the SanSan tile in the Access Panel, you should get automatically signed-on to your SanSan application.</span><span class="sxs-lookup"><span data-stu-id="09cb7-236">When you click the SanSan tile in the Access Panel, you should get automatically signed-on to your SanSan application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="09cb7-237">Additional resources</span><span class="sxs-lookup"><span data-stu-id="09cb7-237">Additional resources</span></span>
* [<span data-ttu-id="09cb7-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09cb7-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="09cb7-239">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="09cb7-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-sansan-tutorial/tutorial_general_205.png


























