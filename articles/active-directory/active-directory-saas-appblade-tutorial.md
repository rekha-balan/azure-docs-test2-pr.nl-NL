---
title: 'Tutorial: Azure Active Directory integration with AppBlade | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and AppBlade.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 3360d7aa-6518-4f99-88bd-b7f7258183e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 94a400aff65580c8595c5b27cc92a6505fb41b4e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662182"
---
# <a name="tutorial-azure-active-directory-integration-with-appblade"></a><span data-ttu-id="bc897-103">Tutorial: Azure Active Directory integration with AppBlade</span><span class="sxs-lookup"><span data-stu-id="bc897-103">Tutorial: Azure Active Directory integration with AppBlade</span></span>
<span data-ttu-id="bc897-104">The objective of this tutorial is to show you how to integrate AppBlade with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bc897-104">The objective of this tutorial is to show you how to integrate AppBlade with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="bc897-105">Integrating AppBlade with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="bc897-105">Integrating AppBlade with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="bc897-106">You can control in Azure AD who has access to AppBlade</span><span class="sxs-lookup"><span data-stu-id="bc897-106">You can control in Azure AD who has access to AppBlade</span></span>
* <span data-ttu-id="bc897-107">You can enable your users to automatically get signed-on to AppBlade (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="bc897-107">You can enable your users to automatically get signed-on to AppBlade (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="bc897-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="bc897-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="bc897-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bc897-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc897-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bc897-110">Prerequisites</span></span>
<span data-ttu-id="bc897-111">To configure Azure AD integration with AppBlade, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="bc897-111">To configure Azure AD integration with AppBlade, you need the following items:</span></span>

* <span data-ttu-id="bc897-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="bc897-112">An Azure AD subscription</span></span>
* <span data-ttu-id="bc897-113">A AppBlade single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="bc897-113">A AppBlade single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bc897-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="bc897-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="bc897-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="bc897-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="bc897-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="bc897-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="bc897-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bc897-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bc897-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="bc897-118">Scenario Description</span></span>
<span data-ttu-id="bc897-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="bc897-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="bc897-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="bc897-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bc897-121">Adding AppBlade from the gallery</span><span class="sxs-lookup"><span data-stu-id="bc897-121">Adding AppBlade from the gallery</span></span>
2. <span data-ttu-id="bc897-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bc897-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appblade-from-the-gallery"></a><span data-ttu-id="bc897-123">Adding AppBlade from the gallery</span><span class="sxs-lookup"><span data-stu-id="bc897-123">Adding AppBlade from the gallery</span></span>
<span data-ttu-id="bc897-124">To configure the integration of AppBlade into Azure AD, you need to add AppBlade from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="bc897-124">To configure the integration of AppBlade into Azure AD, you need to add AppBlade from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bc897-125">**To add AppBlade from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bc897-125">**To add AppBlade from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bc897-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bc897-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="bc897-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="bc897-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="bc897-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="bc897-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="bc897-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="bc897-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="bc897-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="bc897-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="bc897-135">In the search box, type **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="bc897-135">In the search box, type **AppBlade**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/tutorial_appblade_01.png)

1. <span data-ttu-id="bc897-137">In the results pane, select **AppBlade**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="bc897-137">In the results pane, select **AppBlade**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/tutorial_appblade_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bc897-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="bc897-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bc897-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with AppBlade based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="bc897-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with AppBlade based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bc897-141">For single sign-on to work, Azure AD needs to know what the counterpart user in AppBlade to a user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="bc897-141">For single sign-on to work, Azure AD needs to know what the counterpart user in AppBlade to a user in Azure AD is.</span></span> <span data-ttu-id="bc897-142">In other words, a link relationship between an Azure AD user and the related user in AppBlade needs to be established.</span><span class="sxs-lookup"><span data-stu-id="bc897-142">In other words, a link relationship between an Azure AD user and the related user in AppBlade needs to be established.</span></span>  
<span data-ttu-id="bc897-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in AppBlade.</span><span class="sxs-lookup"><span data-stu-id="bc897-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in AppBlade.</span></span>

<span data-ttu-id="bc897-144">To configure and test Azure AD single sign-on with AppBlade, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="bc897-144">To configure and test Azure AD single sign-on with AppBlade, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bc897-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="bc897-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bc897-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bc897-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bc897-147">**[Creating a AppBlade test user](#creating-a-appblade-test-user)** - to have a counterpart of Britta Simon in AppBlade that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="bc897-147">**[Creating a AppBlade test user](#creating-a-appblade-test-user)** - to have a counterpart of Britta Simon in AppBlade that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="bc897-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="bc897-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bc897-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="bc897-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bc897-150">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bc897-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="bc897-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your AppBlade application.</span><span class="sxs-lookup"><span data-stu-id="bc897-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your AppBlade application.</span></span>

<span data-ttu-id="bc897-152">**To configure Azure AD single sign-on with AppBlade, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bc897-152">**To configure Azure AD single sign-on with AppBlade, perform the following steps:**</span></span>

1. <span data-ttu-id="bc897-153">In the Azure classic portal, on the **AppBlade** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="bc897-153">In the Azure classic portal, on the **AppBlade** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="bc897-155">On the **How would you like users to sign on to AppBlade** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bc897-155">On the **How would you like users to sign on to AppBlade** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/tutorial_appblade_03.png) >
3. <span data-ttu-id="bc897-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bc897-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/tutorial_appblade_04.png) 

    <span data-ttu-id="bc897-159">a.</span><span class="sxs-lookup"><span data-stu-id="bc897-159">a.</span></span> <span data-ttu-id="bc897-160">In the Sign On URL textbox, type the URL used by your users to sign-on to your AppBlade application using the following pattern: **“https://companyname.appblade.com/saml/tenantid”**.</span><span class="sxs-lookup"><span data-stu-id="bc897-160">In the Sign On URL textbox, type the URL used by your users to sign-on to your AppBlade application using the following pattern: **“https://companyname.appblade.com/saml/tenantid”**.</span></span>

    <span data-ttu-id="bc897-161">b.</span><span class="sxs-lookup"><span data-stu-id="bc897-161">b.</span></span> <span data-ttu-id="bc897-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bc897-162">Click **Next**.</span></span>


1. <span data-ttu-id="bc897-163">On the **Configure single sign-on at AppBlade** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bc897-163">On the **Configure single sign-on at AppBlade** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/tutorial_appblade_05.png) 
   
    <span data-ttu-id="bc897-165">a.</span><span class="sxs-lookup"><span data-stu-id="bc897-165">a.</span></span> <span data-ttu-id="bc897-166">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="bc897-166">Click **Download metadata**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="bc897-167">b.</span><span class="sxs-lookup"><span data-stu-id="bc897-167">b.</span></span> <span data-ttu-id="bc897-168">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bc897-168">Click **Next**.</span></span>
2. <span data-ttu-id="bc897-169">To get SSO configured for your application, contact your AppBlade support team via **support@appblade.com** and attach the downloaded metadata file to your email.</span><span class="sxs-lookup"><span data-stu-id="bc897-169">To get SSO configured for your application, contact your AppBlade support team via **support@appblade.com** and attach the downloaded metadata file to your email.</span></span> <span data-ttu-id="bc897-170">Also, please ask them to configure the **SSO Issuer URL** as **https://appblade.com/saml**.</span><span class="sxs-lookup"><span data-stu-id="bc897-170">Also, please ask them to configure the **SSO Issuer URL** as **https://appblade.com/saml**.</span></span> <span data-ttu-id="bc897-171">This setting is required for single sign-on to work.</span><span class="sxs-lookup"><span data-stu-id="bc897-171">This setting is required for single sign-on to work.</span></span>
3. <span data-ttu-id="bc897-172">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bc897-172">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
4. <span data-ttu-id="bc897-174">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="bc897-174">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bc897-176">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="bc897-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="bc897-177">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bc897-177">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Create Azure AD User][20]

<span data-ttu-id="bc897-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bc897-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bc897-180">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bc897-180">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="bc897-182">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="bc897-182">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="bc897-183">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="bc897-183">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="bc897-185">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="bc897-185">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="bc897-187">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bc897-187">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="bc897-189">a.</span><span class="sxs-lookup"><span data-stu-id="bc897-189">a.</span></span> <span data-ttu-id="bc897-190">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="bc897-190">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="bc897-191">b.</span><span class="sxs-lookup"><span data-stu-id="bc897-191">b.</span></span> <span data-ttu-id="bc897-192">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bc897-192">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="bc897-193">c.</span><span class="sxs-lookup"><span data-stu-id="bc897-193">c.</span></span> <span data-ttu-id="bc897-194">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bc897-194">Click **Next**.</span></span>
6. <span data-ttu-id="bc897-195">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bc897-195">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="bc897-197">a.</span><span class="sxs-lookup"><span data-stu-id="bc897-197">a.</span></span> <span data-ttu-id="bc897-198">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="bc897-198">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="bc897-199">b.</span><span class="sxs-lookup"><span data-stu-id="bc897-199">b.</span></span> <span data-ttu-id="bc897-200">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="bc897-200">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="bc897-201">c.</span><span class="sxs-lookup"><span data-stu-id="bc897-201">c.</span></span> <span data-ttu-id="bc897-202">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="bc897-202">In the **Display Name** textbox, type **Britta Simon**.</span></span>
    
    <span data-ttu-id="bc897-203">d.</span><span class="sxs-lookup"><span data-stu-id="bc897-203">d.</span></span> <span data-ttu-id="bc897-204">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="bc897-204">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="bc897-205">e.</span><span class="sxs-lookup"><span data-stu-id="bc897-205">e.</span></span> <span data-ttu-id="bc897-206">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="bc897-206">Click **Next**.</span></span>

7. <span data-ttu-id="bc897-207">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="bc897-207">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="bc897-209">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="bc897-209">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="bc897-211">a.</span><span class="sxs-lookup"><span data-stu-id="bc897-211">a.</span></span> <span data-ttu-id="bc897-212">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="bc897-212">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="bc897-213">b.</span><span class="sxs-lookup"><span data-stu-id="bc897-213">b.</span></span> <span data-ttu-id="bc897-214">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="bc897-214">Click **Complete**.</span></span>   

### <a name="creating-a-appblade-test-user"></a><span data-ttu-id="bc897-215">Creating a AppBlade test user</span><span class="sxs-lookup"><span data-stu-id="bc897-215">Creating a AppBlade test user</span></span>
<span data-ttu-id="bc897-216">The objective of this section is to create a user called Britta Simon in AppBlade.</span><span class="sxs-lookup"><span data-stu-id="bc897-216">The objective of this section is to create a user called Britta Simon in AppBlade.</span></span> <span data-ttu-id="bc897-217">AppBlade supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="bc897-217">AppBlade supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="bc897-218">**Please make sure that your domain name is configured with AppBlade for user provisoning. After that only the just-in-time user provisioning will work.**</span><span class="sxs-lookup"><span data-stu-id="bc897-218">**Please make sure that your domain name is configured with AppBlade for user provisoning. After that only the just-in-time user provisioning will work.**</span></span>

<span data-ttu-id="bc897-219">If the user has an email address ending with the domain configured by AppBlade for your account then the user will automatically join the account as a member with the permission level you specify, which is one of "Basic" (a basic user who can only install applications), "Team Member" (a user who can upload new app versions and manage projects), or "Administrator" (full admin privileges to the account).</span><span class="sxs-lookup"><span data-stu-id="bc897-219">If the user has an email address ending with the domain configured by AppBlade for your account then the user will automatically join the account as a member with the permission level you specify, which is one of "Basic" (a basic user who can only install applications), "Team Member" (a user who can upload new app versions and manage projects), or "Administrator" (full admin privileges to the account).</span></span> <span data-ttu-id="bc897-220">Normally one would choose Basic and then promote users manually via an Admin login (AppBlade needs to configure either an email-based admin login in advance or promote a user on behalf of the customer after login).</span><span class="sxs-lookup"><span data-stu-id="bc897-220">Normally one would choose Basic and then promote users manually via an Admin login (AppBlade needs to configure either an email-based admin login in advance or promote a user on behalf of the customer after login).</span></span>

<span data-ttu-id="bc897-221">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="bc897-221">There is no action item for you in this section.</span></span> <span data-ttu-id="bc897-222">A new user will be created during an attempt to access AppBlade if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="bc897-222">A new user will be created during an attempt to access AppBlade if it doesn't exist yet.</span></span> <span data-ttu-id="bc897-223">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="bc897-223">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

> [!NOTE]
> <span data-ttu-id="bc897-224">If you need to create a user manually, you need to contact the AppBlade support team.</span><span class="sxs-lookup"><span data-stu-id="bc897-224">If you need to create a user manually, you need to contact the AppBlade support team.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bc897-225">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="bc897-225">Assigning the Azure AD test user</span></span>
<span data-ttu-id="bc897-226">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to AppBlade.</span><span class="sxs-lookup"><span data-stu-id="bc897-226">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to AppBlade.</span></span>

![Assign User][200] 

<span data-ttu-id="bc897-228">**To assign Britta Simon to AppBlade, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="bc897-228">**To assign Britta Simon to AppBlade, perform the following steps:**</span></span>

1. <span data-ttu-id="bc897-229">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="bc897-229">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="bc897-231">In the applications list, select **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="bc897-231">In the applications list, select **AppBlade**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/tutorial_appblade_50.png) 
3. <span data-ttu-id="bc897-233">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="bc897-233">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="bc897-235">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="bc897-235">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="bc897-236">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="bc897-236">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="bc897-238">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="bc897-238">Testing Single Sign-On</span></span>
<span data-ttu-id="bc897-239">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="bc897-239">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="bc897-240">When you click the AppBlade tile in the Access Panel, you should get automatically signed-on to your AppBlade application.</span><span class="sxs-lookup"><span data-stu-id="bc897-240">When you click the AppBlade tile in the Access Panel, you should get automatically signed-on to your AppBlade application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bc897-241">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="bc897-241">Additional Resources</span></span>
* [<span data-ttu-id="bc897-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bc897-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bc897-243">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bc897-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-appblade-tutorial/tutorial_general_205.png

























