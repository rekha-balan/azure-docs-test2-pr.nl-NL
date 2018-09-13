---
title: 'Tutorial: Azure Active Directory integration with Trakstar | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Trakstar.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 411cb8c3-95c6-4138-acf2-ffc7f663e89a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0adfc545860ec8ddf2149023f364cbea3b47422e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556302"
---
# <a name="tutorial-azure-active-directory-integration-with-trakstar"></a><span data-ttu-id="e2df8-103">Tutorial: Azure Active Directory integration with Trakstar</span><span class="sxs-lookup"><span data-stu-id="e2df8-103">Tutorial: Azure Active Directory integration with Trakstar</span></span>
<span data-ttu-id="e2df8-104">The objective of this tutorial is to show you how to integrate Trakstar with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e2df8-104">The objective of this tutorial is to show you how to integrate Trakstar with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="e2df8-105">Integrating Trakstar with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="e2df8-105">Integrating Trakstar with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="e2df8-106">You can control in Azure AD who has access to Trakstar</span><span class="sxs-lookup"><span data-stu-id="e2df8-106">You can control in Azure AD who has access to Trakstar</span></span>
* <span data-ttu-id="e2df8-107">You can enable your users to automatically get signed-on to Trakstar (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="e2df8-107">You can enable your users to automatically get signed-on to Trakstar (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="e2df8-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="e2df8-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="e2df8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e2df8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2df8-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e2df8-110">Prerequisites</span></span>
<span data-ttu-id="e2df8-111">To configure Azure AD integration with Trakstar, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="e2df8-111">To configure Azure AD integration with Trakstar, you need the following items:</span></span>

* <span data-ttu-id="e2df8-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="e2df8-112">An Azure AD subscription</span></span>
* <span data-ttu-id="e2df8-113">A Trakstar single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="e2df8-113">A Trakstar single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e2df8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="e2df8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="e2df8-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="e2df8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="e2df8-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="e2df8-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="e2df8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e2df8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e2df8-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="e2df8-118">Scenario Description</span></span>
<span data-ttu-id="e2df8-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="e2df8-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="e2df8-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="e2df8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e2df8-121">Adding Trakstar from the gallery</span><span class="sxs-lookup"><span data-stu-id="e2df8-121">Adding Trakstar from the gallery</span></span>
2. <span data-ttu-id="e2df8-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e2df8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trakstar-from-the-gallery"></a><span data-ttu-id="e2df8-123">Adding Trakstar from the gallery</span><span class="sxs-lookup"><span data-stu-id="e2df8-123">Adding Trakstar from the gallery</span></span>
<span data-ttu-id="e2df8-124">To configure the integration of Trakstar into Azure AD, you need to add Trakstar from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="e2df8-124">To configure the integration of Trakstar into Azure AD, you need to add Trakstar from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e2df8-125">**To add Trakstar from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e2df8-125">**To add Trakstar from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e2df8-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="e2df8-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="e2df8-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="e2df8-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="e2df8-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="e2df8-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="e2df8-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="e2df8-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="e2df8-135">In the search box, type **Trakstar**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-135">In the search box, type **Trakstar**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_01.png)
7. <span data-ttu-id="e2df8-137">In the results pane, select **Trakstar**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="e2df8-137">In the results pane, select **Trakstar**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e2df8-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e2df8-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e2df8-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Trakstar based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e2df8-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Trakstar based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e2df8-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Trakstar to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="e2df8-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Trakstar to an user in Azure AD is.</span></span> <span data-ttu-id="e2df8-142">In other words, a link relationship between an Azure AD user and the related user in Trakstar needs to be established.</span><span class="sxs-lookup"><span data-stu-id="e2df8-142">In other words, a link relationship between an Azure AD user and the related user in Trakstar needs to be established.</span></span>  
<span data-ttu-id="e2df8-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Trakstar.</span><span class="sxs-lookup"><span data-stu-id="e2df8-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Trakstar.</span></span>

<span data-ttu-id="e2df8-144">To configure and test Azure AD single sign-on with Trakstar, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e2df8-144">To configure and test Azure AD single sign-on with Trakstar, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e2df8-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="e2df8-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e2df8-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e2df8-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e2df8-147">**[Creating a Trakstar test user](#creating-a-Trakstar-test-user)** - to have a counterpart of Britta Simon in Trakstar that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="e2df8-147">**[Creating a Trakstar test user](#creating-a-Trakstar-test-user)** - to have a counterpart of Britta Simon in Trakstar that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="e2df8-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e2df8-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e2df8-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="e2df8-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e2df8-150">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e2df8-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="e2df8-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Trakstar application.</span><span class="sxs-lookup"><span data-stu-id="e2df8-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Trakstar application.</span></span>

<span data-ttu-id="e2df8-152">**To configure Azure AD single sign-on with Trakstar, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e2df8-152">**To configure Azure AD single sign-on with Trakstar, perform the following steps:**</span></span>

1. <span data-ttu-id="e2df8-153">In the Azure classic portal, on the **Trakstar** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="e2df8-153">In the Azure classic portal, on the **Trakstar** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="e2df8-155">On the **How would you like users to sign on to Trakstar** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-155">On the **How would you like users to sign on to Trakstar** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_03.png) 
3. <span data-ttu-id="e2df8-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e2df8-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_04.png) 

    <span data-ttu-id="e2df8-159">a.</span><span class="sxs-lookup"><span data-stu-id="e2df8-159">a.</span></span> <span data-ttu-id="e2df8-160">In the Sign On URL textbox, type the URL used by your users to sign-on to your Trakstar application using the following pattern: **“https://app.trakstar.com/auth/saml/callback?namespace=&lt;name space&gt;”**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-160">In the Sign On URL textbox, type the URL used by your users to sign-on to your Trakstar application using the following pattern: **“https://app.trakstar.com/auth/saml/callback?namespace=&lt;name space&gt;”**.</span></span>

    <span data-ttu-id="e2df8-161">b.</span><span class="sxs-lookup"><span data-stu-id="e2df8-161">b.</span></span> <span data-ttu-id="e2df8-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-162">Click **Next**.</span></span>

1. <span data-ttu-id="e2df8-163">On the **Configure single sign-on at Trakstar** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e2df8-163">On the **Configure single sign-on at Trakstar** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_05.png) 
   
    <span data-ttu-id="e2df8-165">a.</span><span class="sxs-lookup"><span data-stu-id="e2df8-165">a.</span></span> <span data-ttu-id="e2df8-166">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="e2df8-166">Click **Download certificate**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="e2df8-167">b.</span><span class="sxs-lookup"><span data-stu-id="e2df8-167">b.</span></span> <span data-ttu-id="e2df8-168">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-168">Click **Next**.</span></span>
2. <span data-ttu-id="e2df8-169">To get SSO configured for your application, contact your Trakstar support team via [integrations@trakstar.com](mailto:integrations@trakstar.com) and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="e2df8-169">To get SSO configured for your application, contact your Trakstar support team via [integrations@trakstar.com](mailto:integrations@trakstar.com) and provide them with the following:</span></span>
   
   * <span data-ttu-id="e2df8-170">The downloaded certificate file</span><span class="sxs-lookup"><span data-stu-id="e2df8-170">The downloaded certificate file</span></span>
   * <span data-ttu-id="e2df8-171">The **Issuer URL**</span><span class="sxs-lookup"><span data-stu-id="e2df8-171">The **Issuer URL**</span></span>
   * <span data-ttu-id="e2df8-172">The **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="e2df8-172">The **SAML SSO URL**</span></span>
   * <span data-ttu-id="e2df8-173">The **Single Sign-Out Service URL**</span><span class="sxs-lookup"><span data-stu-id="e2df8-173">The **Single Sign-Out Service URL**</span></span>
3. <span data-ttu-id="e2df8-174">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-174">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
4. <span data-ttu-id="e2df8-176">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-176">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e2df8-178">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e2df8-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="e2df8-179">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e2df8-179">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Create Azure AD User][20]

<span data-ttu-id="e2df8-181">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e2df8-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e2df8-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="e2df8-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="e2df8-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="e2df8-185">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-185">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="e2df8-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="e2df8-189">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e2df8-189">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="e2df8-191">a.</span><span class="sxs-lookup"><span data-stu-id="e2df8-191">a.</span></span> <span data-ttu-id="e2df8-192">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="e2df8-192">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="e2df8-193">b.</span><span class="sxs-lookup"><span data-stu-id="e2df8-193">b.</span></span> <span data-ttu-id="e2df8-194">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-194">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="e2df8-195">c.</span><span class="sxs-lookup"><span data-stu-id="e2df8-195">c.</span></span> <span data-ttu-id="e2df8-196">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-196">Click **Next**.</span></span>
6. <span data-ttu-id="e2df8-197">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e2df8-197">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="e2df8-199">a.</span><span class="sxs-lookup"><span data-stu-id="e2df8-199">a.</span></span> <span data-ttu-id="e2df8-200">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-200">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="e2df8-201">b.</span><span class="sxs-lookup"><span data-stu-id="e2df8-201">b.</span></span> <span data-ttu-id="e2df8-202">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-202">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="e2df8-203">c.</span><span class="sxs-lookup"><span data-stu-id="e2df8-203">c.</span></span> <span data-ttu-id="e2df8-204">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-204">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="e2df8-205">d.</span><span class="sxs-lookup"><span data-stu-id="e2df8-205">d.</span></span> <span data-ttu-id="e2df8-206">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-206">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="e2df8-207">e.</span><span class="sxs-lookup"><span data-stu-id="e2df8-207">e.</span></span> <span data-ttu-id="e2df8-208">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-208">Click **Next**.</span></span>

7. <span data-ttu-id="e2df8-209">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-209">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="e2df8-211">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e2df8-211">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="e2df8-213">a.</span><span class="sxs-lookup"><span data-stu-id="e2df8-213">a.</span></span> <span data-ttu-id="e2df8-214">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-214">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="e2df8-215">b.</span><span class="sxs-lookup"><span data-stu-id="e2df8-215">b.</span></span> <span data-ttu-id="e2df8-216">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-216">Click **Complete**.</span></span>   

### <a name="creating-a-trakstar-test-user"></a><span data-ttu-id="e2df8-217">Creating a Trakstar test user</span><span class="sxs-lookup"><span data-stu-id="e2df8-217">Creating a Trakstar test user</span></span>
<span data-ttu-id="e2df8-218">The objective of this section is to create a user called Britta Simon in Trakstar.</span><span class="sxs-lookup"><span data-stu-id="e2df8-218">The objective of this section is to create a user called Britta Simon in Trakstar.</span></span> <span data-ttu-id="e2df8-219">Please work with Trakstar support team to add the users in the Trakstar account.</span><span class="sxs-lookup"><span data-stu-id="e2df8-219">Please work with Trakstar support team to add the users in the Trakstar account.</span></span> 

> [!NOTE]
> <span data-ttu-id="e2df8-220">If you need to create an user manually, you need to contact the Trakstar support team.</span><span class="sxs-lookup"><span data-stu-id="e2df8-220">If you need to create an user manually, you need to contact the Trakstar support team.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e2df8-221">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e2df8-221">Assigning the Azure AD test user</span></span>
<span data-ttu-id="e2df8-222">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Trakstar.</span><span class="sxs-lookup"><span data-stu-id="e2df8-222">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Trakstar.</span></span>

![Assign User][200] 

<span data-ttu-id="e2df8-224">**To assign Britta Simon to Trakstar, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e2df8-224">**To assign Britta Simon to Trakstar, perform the following steps:**</span></span>

1. <span data-ttu-id="e2df8-225">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="e2df8-225">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="e2df8-227">In the applications list, select **Trakstar**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-227">In the applications list, select **Trakstar**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/tutorial_trakstar_50.png) 
3. <span data-ttu-id="e2df8-229">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-229">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="e2df8-231">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-231">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="e2df8-232">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="e2df8-232">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="e2df8-234">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="e2df8-234">Testing Single Sign-On</span></span>
<span data-ttu-id="e2df8-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="e2df8-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="e2df8-236">When you click the Trakstar tile in the Access Panel, you should get automatically signed-on to your Trakstar application.</span><span class="sxs-lookup"><span data-stu-id="e2df8-236">When you click the Trakstar tile in the Access Panel, you should get automatically signed-on to your Trakstar application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e2df8-237">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="e2df8-237">Additional Resources</span></span>
* [<span data-ttu-id="e2df8-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e2df8-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e2df8-239">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e2df8-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-trakstar-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakstar-tutorial/tutorial_general_205.png

























