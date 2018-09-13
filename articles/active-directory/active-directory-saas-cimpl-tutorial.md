---
title: 'Tutorial: Azure Active Directory integration with Cimpl | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Cimpl.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 58ee5481-ae40-4e4a-a3c9-86343851fc9a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: jeedes
ms.openlocfilehash: d5ffe13e4e0641a1e8dd99f9aece3cab98e9733e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563899"
---
# <a name="tutorial-azure-active-directory-integration-with-cimpl"></a><span data-ttu-id="7ab3b-103">Tutorial: Azure Active Directory integration with Cimpl</span><span class="sxs-lookup"><span data-stu-id="7ab3b-103">Tutorial: Azure Active Directory integration with Cimpl</span></span>
<span data-ttu-id="7ab3b-104">The objective of this tutorial is to show you how to integrate Cimpl with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7ab3b-104">The objective of this tutorial is to show you how to integrate Cimpl with Azure Active Directory (Azure AD).</span></span>  

<span data-ttu-id="7ab3b-105">Integrating Cimpl with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7ab3b-105">Integrating Cimpl with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="7ab3b-106">You can control in Azure AD who has access to Cimpl</span><span class="sxs-lookup"><span data-stu-id="7ab3b-106">You can control in Azure AD who has access to Cimpl</span></span>
* <span data-ttu-id="7ab3b-107">You can enable your users to automatically get signed-on to Cimpl single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="7ab3b-107">You can enable your users to automatically get signed-on to Cimpl single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="7ab3b-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="7ab3b-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="7ab3b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7ab3b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ab3b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7ab3b-110">Prerequisites</span></span>
<span data-ttu-id="7ab3b-111">To configure Azure AD integration with Cimpl, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7ab3b-111">To configure Azure AD integration with Cimpl, you need the following items:</span></span>

* <span data-ttu-id="7ab3b-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7ab3b-112">An Azure AD subscription</span></span>
* <span data-ttu-id="7ab3b-113">A Cimpl single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7ab3b-113">A Cimpl single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="7ab3b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="7ab3b-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7ab3b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="7ab3b-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="7ab3b-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7ab3b-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7ab3b-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="7ab3b-118">Scenario Description</span></span>
<span data-ttu-id="7ab3b-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>  

<span data-ttu-id="7ab3b-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7ab3b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7ab3b-121">Adding Cimpl from the gallery</span><span class="sxs-lookup"><span data-stu-id="7ab3b-121">Adding Cimpl from the gallery</span></span>
2. <span data-ttu-id="7ab3b-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="7ab3b-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-cimpl-from-the-gallery"></a><span data-ttu-id="7ab3b-123">Adding Cimpl from the gallery</span><span class="sxs-lookup"><span data-stu-id="7ab3b-123">Adding Cimpl from the gallery</span></span>
<span data-ttu-id="7ab3b-124">To configure the integration of Cimpl into Azure AD, you need to add Cimpl from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-124">To configure the integration of Cimpl into Azure AD, you need to add Cimpl from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7ab3b-125">**To add Cimpl from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7ab3b-125">**To add Cimpl from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7ab3b-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="7ab3b-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="7ab3b-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="7ab3b-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="7ab3b-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="7ab3b-135">In the search box, type **Cimpl**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-135">In the search box, type **Cimpl**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_01.png)
7. <span data-ttu-id="7ab3b-137">In the results pane, select **Cimpl**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-137">In the results pane, select **Cimpl**, and then click **Complete** to add the application.</span></span>

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="7ab3b-138">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="7ab3b-138">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="7ab3b-139">The objective of this section is to show you how to configure and test Azure AD SSO with Cimpl based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7ab3b-139">The objective of this section is to show you how to configure and test Azure AD SSO with Cimpl based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7ab3b-140">For SSO to work, Azure AD needs to know what the counterpart user in Cimpl to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-140">For SSO to work, Azure AD needs to know what the counterpart user in Cimpl to an user in Azure AD is.</span></span> <span data-ttu-id="7ab3b-141">In other words, a link relationship between an Azure AD user and the related user in Cimpl needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-141">In other words, a link relationship between an Azure AD user and the related user in Cimpl needs to be established.</span></span> 

<span data-ttu-id="7ab3b-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Cimpl.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Cimpl.</span></span>

<span data-ttu-id="7ab3b-143">To configure and test Azure AD SSO with Cimpl, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7ab3b-143">To configure and test Azure AD SSO with Cimpl, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7ab3b-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7ab3b-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7ab3b-146">**[Creating a Cimpl test user](#creating-a-cimpl-test-user)** - to have a counterpart of Britta Simon in Cimpl that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-146">**[Creating a Cimpl test user](#creating-a-cimpl-test-user)** - to have a counterpart of Britta Simon in Cimpl that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="7ab3b-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7ab3b-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="7ab3b-149">Configuring Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="7ab3b-149">Configuring Azure AD SSO</span></span>
<span data-ttu-id="7ab3b-150">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Cimpl application.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-150">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Cimpl application.</span></span>

<span data-ttu-id="7ab3b-151">**To configure Azure AD SSO with Cimpl, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7ab3b-151">**To configure Azure AD SSO with Cimpl, perform the following steps:**</span></span>

1. <span data-ttu-id="7ab3b-152">In the Azure classic portal, on the **Cimpl** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-152">In the Azure classic portal, on the **Cimpl** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="7ab3b-154">On the **How would you like users to sign on to Cimpl** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-154">On the **How would you like users to sign on to Cimpl** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_03.png) 
3. <span data-ttu-id="7ab3b-156">On the **Configure App Settings** dialog page, perform the following steps:.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-156">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_04.png) 
  * <span data-ttu-id="7ab3b-158">In the Sign On URL textbox, type the URL used by your users to sign-on to your Cimpl application using the following pattern: “https://login.bws.cimpl.com/SAMLSSO/Service.aspx?cimpl.idpid=\<TENANT ID PID\>”.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-158">In the Sign On URL textbox, type the URL used by your users to sign-on to your Cimpl application using the following pattern: “https://login.bws.cimpl.com/SAMLSSO/Service.aspx?cimpl.idpid=\<TENANT ID PID\>”.</span></span>
4. <span data-ttu-id="7ab3b-159">On the **Configure single sign-on at Cimpl** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7ab3b-159">On the **Configure single sign-on at Cimpl** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_05.png) 
  1. <span data-ttu-id="7ab3b-161">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-161">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="7ab3b-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-162">Click **Next**.</span></span>
2. <span data-ttu-id="7ab3b-163">To get SSO configured for your application, contact your Cimpl support team on +1 866-982-8250 and email the attach downloaded certificate file.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-163">To get SSO configured for your application, contact your Cimpl support team on +1 866-982-8250 and email the attach downloaded certificate file.</span></span> <span data-ttu-id="7ab3b-164">Also please do provide the Identity Provider ID and Remote Login URL so that they can be configured for SSO integration.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-164">Also please do provide the Identity Provider ID and Remote Login URL so that they can be configured for SSO integration.</span></span>
3. <span data-ttu-id="7ab3b-165">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-165">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
4. <span data-ttu-id="7ab3b-167">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-167">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7ab3b-169">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7ab3b-169">Create an Azure AD test user</span></span>
<span data-ttu-id="7ab3b-170">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-170">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Create Azure AD User][20]

<span data-ttu-id="7ab3b-172">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7ab3b-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7ab3b-173">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-173">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="7ab3b-175">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-175">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="7ab3b-176">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-176">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="7ab3b-178">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-178">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="7ab3b-180">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7ab3b-180">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="7ab3b-182">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-182">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="7ab3b-183">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-183">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="7ab3b-184">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-184">Click **Next**.</span></span>
6. <span data-ttu-id="7ab3b-185">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7ab3b-185">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="7ab3b-187">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-187">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="7ab3b-188">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-188">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="7ab3b-189">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-189">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="7ab3b-190">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-190">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="7ab3b-191">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-191">Click **Next**.</span></span>
7. <span data-ttu-id="7ab3b-192">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-192">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="7ab3b-194">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7ab3b-194">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="7ab3b-196">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-196">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="7ab3b-197">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-197">Click **Complete**.</span></span>   

### <a name="create-a-cimpl-test-user"></a><span data-ttu-id="7ab3b-198">Create a Cimpl test user</span><span class="sxs-lookup"><span data-stu-id="7ab3b-198">Create a Cimpl test user</span></span>
<span data-ttu-id="7ab3b-199">The objective of this section is to create a user called Britta Simon in Cimpl.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-199">The objective of this section is to create a user called Britta Simon in Cimpl.</span></span> <span data-ttu-id="7ab3b-200">Please work with Cimpl support team to add the users in the Cimpl account.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-200">Please work with Cimpl support team to add the users in the Cimpl account.</span></span> 

>[!NOTE]
><span data-ttu-id="7ab3b-201">If you need to create an user manually, you need to contact the Cimpl support team.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-201">If you need to create an user manually, you need to contact the Cimpl support team.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7ab3b-202">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7ab3b-202">Assign the Azure AD test user</span></span>
<span data-ttu-id="7ab3b-203">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Cimpl.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-203">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Cimpl.</span></span>

![Assign User][200] 

<span data-ttu-id="7ab3b-205">**To assign Britta Simon to Cimpl, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7ab3b-205">**To assign Britta Simon to Cimpl, perform the following steps:**</span></span>

1. <span data-ttu-id="7ab3b-206">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-206">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="7ab3b-208">In the applications list, select **Cimpl**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-208">In the applications list, select **Cimpl**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/tutorial_cimpl_50.png) 
3. <span data-ttu-id="7ab3b-210">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-210">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="7ab3b-212">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-212">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="7ab3b-213">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-213">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="7ab3b-215">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="7ab3b-215">Test single sign-on</span></span>
<span data-ttu-id="7ab3b-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  <span data-ttu-id="7ab3b-217">When you click the Cimpl tile in the Access Panel, you should get automatically signed-on to your Cimpl application.</span><span class="sxs-lookup"><span data-stu-id="7ab3b-217">When you click the Cimpl tile in the Access Panel, you should get automatically signed-on to your Cimpl application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7ab3b-218">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="7ab3b-218">Additional Resources</span></span>
* [<span data-ttu-id="7ab3b-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ab3b-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7ab3b-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7ab3b-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-cimpl-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-cimpl-tutorial/tutorial_general_205.png
























