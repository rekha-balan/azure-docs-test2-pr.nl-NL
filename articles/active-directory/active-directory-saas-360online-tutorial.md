---
title: 'Tutorial: Azure Active Directory integration with  360 Online | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and 360 Online.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: cda8eba6-843f-4a09-8c55-0aaf6e593d75
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: c20d8ee431e6d87ab7fe01a0552c9528c22ead42
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553165"
---
# <a name="tutorial-azure-active-directory-integration-with-360-online"></a><span data-ttu-id="01c16-103">Tutorial: Azure Active Directory integration with 360 Online</span><span class="sxs-lookup"><span data-stu-id="01c16-103">Tutorial: Azure Active Directory integration with 360 Online</span></span>
<span data-ttu-id="01c16-104">The objective of this tutorial is to show you how to integrate 360 Online with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="01c16-104">The objective of this tutorial is to show you how to integrate 360 Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="01c16-105">Integrating 360 Online with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="01c16-105">Integrating 360 Online with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="01c16-106">You can control in Azure AD who has access to 360 Online Server</span><span class="sxs-lookup"><span data-stu-id="01c16-106">You can control in Azure AD who has access to 360 Online Server</span></span>
* <span data-ttu-id="01c16-107">You can enable your users to automatically get signed-on to 360 Online (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="01c16-107">You can enable your users to automatically get signed-on to 360 Online (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="01c16-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="01c16-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="01c16-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="01c16-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01c16-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="01c16-110">Prerequisites</span></span>
<span data-ttu-id="01c16-111">To configure Azure AD integration with 360 Online, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="01c16-111">To configure Azure AD integration with 360 Online, you need the following items:</span></span>

* <span data-ttu-id="01c16-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="01c16-112">An Azure AD subscription</span></span>
* <span data-ttu-id="01c16-113">A 360 Online tenant</span><span class="sxs-lookup"><span data-stu-id="01c16-113">A 360 Online tenant</span></span>

> [!NOTE]
> <span data-ttu-id="01c16-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="01c16-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="01c16-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="01c16-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="01c16-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="01c16-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="01c16-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="01c16-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="01c16-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="01c16-118">Scenario Description</span></span>
<span data-ttu-id="01c16-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="01c16-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="01c16-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="01c16-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="01c16-121">Adding 360 Online from the gallery</span><span class="sxs-lookup"><span data-stu-id="01c16-121">Adding 360 Online from the gallery</span></span>
2. <span data-ttu-id="01c16-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="01c16-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-360-online-from-the-gallery"></a><span data-ttu-id="01c16-123">Adding 360 Online from the gallery</span><span class="sxs-lookup"><span data-stu-id="01c16-123">Adding 360 Online from the gallery</span></span>
<span data-ttu-id="01c16-124">To configure the integration of 360 Online into Azure AD, you need to add 360 Online from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="01c16-124">To configure the integration of 360 Online into Azure AD, you need to add 360 Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="01c16-125">**To add 360 Online from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="01c16-125">**To add 360 Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="01c16-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="01c16-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="01c16-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="01c16-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="01c16-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="01c16-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="01c16-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="01c16-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="01c16-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="01c16-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="01c16-135">In the search box, type **360 Online**.</span><span class="sxs-lookup"><span data-stu-id="01c16-135">In the search box, type **360 Online**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/tutorial_360online_01.png)
7. <span data-ttu-id="01c16-137">In the results pane, select **360 Online**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="01c16-137">In the results pane, select **360 Online**, and then click **Complete** to add the application.</span></span>
   
    ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/tutorial_360online_06.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="01c16-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="01c16-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="01c16-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with 360 Online based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="01c16-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with 360 Online based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="01c16-141">For single sign-on to work, Azure AD needs to know what the counterpart user in 360 Online to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="01c16-141">For single sign-on to work, Azure AD needs to know what the counterpart user in 360 Online to an user in Azure AD is.</span></span> <span data-ttu-id="01c16-142">In other words, a link relationship between an Azure AD user and the related user in 360 Online needs to be established.</span><span class="sxs-lookup"><span data-stu-id="01c16-142">In other words, a link relationship between an Azure AD user and the related user in 360 Online needs to be established.</span></span>

<span data-ttu-id="01c16-143">To configure and test Azure AD single sign-on with 360 Online, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="01c16-143">To configure and test Azure AD single sign-on with 360 Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="01c16-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="01c16-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="01c16-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="01c16-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="01c16-146">**[Creating a 360 Online test user](#creating-a-360-online-test-user)** - to have a counterpart of Britta Simon in 360 Online that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="01c16-146">**[Creating a 360 Online test user](#creating-a-360-online-test-user)** - to have a counterpart of Britta Simon in 360 Online that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="01c16-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="01c16-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="01c16-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="01c16-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="01c16-149">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="01c16-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="01c16-150">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your 360 Online application.</span><span class="sxs-lookup"><span data-stu-id="01c16-150">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your 360 Online application.</span></span>

<span data-ttu-id="01c16-151">**To configure Azure AD single sign-on with 360 Online, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="01c16-151">**To configure Azure AD single sign-on with 360 Online, perform the following steps:**</span></span>

1. <span data-ttu-id="01c16-152">In the Azure classic portal, on the **360 Online** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="01c16-152">In the Azure classic portal, on the **360 Online** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][13] 
2. <span data-ttu-id="01c16-154">On the **How would you like users to sign on to 360 Online** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="01c16-154">On the **How would you like users to sign on to 360 Online** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/tutorial_360online_03.png) 
3. <span data-ttu-id="01c16-156">On the **Configure App URL** dialog page, perform the following steps and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="01c16-156">On the **Configure App URL** dialog page, perform the following steps and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/tutorial_360online_04.png)
   
    <span data-ttu-id="01c16-158">a.</span><span class="sxs-lookup"><span data-stu-id="01c16-158">a.</span></span> <span data-ttu-id="01c16-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your 360 Online application using the following pattern: `https://<company name>.public360online.com`</span><span class="sxs-lookup"><span data-stu-id="01c16-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your 360 Online application using the following pattern: `https://<company name>.public360online.com`</span></span>
   
    <span data-ttu-id="01c16-160">b.</span><span class="sxs-lookup"><span data-stu-id="01c16-160">b.</span></span> <span data-ttu-id="01c16-161">Click **Next**</span><span class="sxs-lookup"><span data-stu-id="01c16-161">Click **Next**</span></span>
4. <span data-ttu-id="01c16-162">On the **Configure App URL** dialog page, perform the following steps and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="01c16-162">On the **Configure App URL** dialog page, perform the following steps and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/tutorial_360online_05.png) 
   
    <span data-ttu-id="01c16-164">a.</span><span class="sxs-lookup"><span data-stu-id="01c16-164">a.</span></span> <span data-ttu-id="01c16-165">Click **Download metadata**, and then save it on your computer.</span><span class="sxs-lookup"><span data-stu-id="01c16-165">Click **Download metadata**, and then save it on your computer.</span></span>
   
    <span data-ttu-id="01c16-166">b.</span><span class="sxs-lookup"><span data-stu-id="01c16-166">b.</span></span> <span data-ttu-id="01c16-167">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="01c16-167">Click **Next**.</span></span>
5. <span data-ttu-id="01c16-168">To get SSO configured for your application, contact your 360 Online support team via [360online@software-innovation.com](mailto:360online@software-innovation.com) and attach the downloaded metadata file to your mail.</span><span class="sxs-lookup"><span data-stu-id="01c16-168">To get SSO configured for your application, contact your 360 Online support team via [360online@software-innovation.com](mailto:360online@software-innovation.com) and attach the downloaded metadata file to your mail.</span></span>
6. <span data-ttu-id="01c16-169">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="01c16-169">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="01c16-171">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="01c16-171">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="01c16-173">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="01c16-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="01c16-174">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="01c16-174">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="01c16-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="01c16-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="01c16-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="01c16-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="01c16-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="01c16-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="01c16-180">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="01c16-180">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="01c16-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="01c16-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="01c16-184">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="01c16-184">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="01c16-186">a.</span><span class="sxs-lookup"><span data-stu-id="01c16-186">a.</span></span> <span data-ttu-id="01c16-187">As **Type Of User**, select **New user in your organization**.</span><span class="sxs-lookup"><span data-stu-id="01c16-187">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="01c16-188">b.</span><span class="sxs-lookup"><span data-stu-id="01c16-188">b.</span></span> <span data-ttu-id="01c16-189">In the **User Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="01c16-189">In the **User Name** textbox, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="01c16-190">c.</span><span class="sxs-lookup"><span data-stu-id="01c16-190">c.</span></span> <span data-ttu-id="01c16-191">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="01c16-191">Click **Next**.</span></span>
6. <span data-ttu-id="01c16-192">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="01c16-192">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="01c16-194">a.</span><span class="sxs-lookup"><span data-stu-id="01c16-194">a.</span></span> <span data-ttu-id="01c16-195">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="01c16-195">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="01c16-196">b.</span><span class="sxs-lookup"><span data-stu-id="01c16-196">b.</span></span> <span data-ttu-id="01c16-197">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="01c16-197">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="01c16-198">c.</span><span class="sxs-lookup"><span data-stu-id="01c16-198">c.</span></span> <span data-ttu-id="01c16-199">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="01c16-199">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="01c16-200">d.</span><span class="sxs-lookup"><span data-stu-id="01c16-200">d.</span></span> <span data-ttu-id="01c16-201">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="01c16-201">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="01c16-202">e.</span><span class="sxs-lookup"><span data-stu-id="01c16-202">e.</span></span> <span data-ttu-id="01c16-203">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="01c16-203">Click **Next**.</span></span>

7. <span data-ttu-id="01c16-204">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="01c16-204">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="01c16-206">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="01c16-206">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="01c16-208">a.</span><span class="sxs-lookup"><span data-stu-id="01c16-208">a.</span></span> <span data-ttu-id="01c16-209">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="01c16-209">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="01c16-210">b.</span><span class="sxs-lookup"><span data-stu-id="01c16-210">b.</span></span> <span data-ttu-id="01c16-211">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="01c16-211">Click **Complete**.</span></span>   

### <a name="creating-a-360-online-test-user"></a><span data-ttu-id="01c16-212">Creating a 360 Online test user</span><span class="sxs-lookup"><span data-stu-id="01c16-212">Creating a 360 Online test user</span></span>
<span data-ttu-id="01c16-213">The objective of this section is to create a user called Britta Simon in 360 Online.</span><span class="sxs-lookup"><span data-stu-id="01c16-213">The objective of this section is to create a user called Britta Simon in 360 Online.</span></span> 

<span data-ttu-id="01c16-214">To get a user in 360 Online created, you need to contact your 360 Online support team via [360online@software-innovation.com](mailto:360online@software-innovation.com).</span><span class="sxs-lookup"><span data-stu-id="01c16-214">To get a user in 360 Online created, you need to contact your 360 Online support team via [360online@software-innovation.com](mailto:360online@software-innovation.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="01c16-215">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="01c16-215">Assigning the Azure AD test user</span></span>
<span data-ttu-id="01c16-216">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to 360 Online.</span><span class="sxs-lookup"><span data-stu-id="01c16-216">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to 360 Online.</span></span>

![Assign User][200] 

<span data-ttu-id="01c16-218">**To assign Britta Simon to 360 Online, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="01c16-218">**To assign Britta Simon to 360 Online, perform the following steps:**</span></span>

1. <span data-ttu-id="01c16-219">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="01c16-219">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="01c16-221">In the applications list, select **360 Online**.</span><span class="sxs-lookup"><span data-stu-id="01c16-221">In the applications list, select **360 Online**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/tutorial_360online_50.png) 
3. <span data-ttu-id="01c16-223">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="01c16-223">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="01c16-225">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="01c16-225">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="01c16-226">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="01c16-226">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="01c16-228">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="01c16-228">Testing Single Sign-On</span></span>
<span data-ttu-id="01c16-229">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="01c16-229">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="01c16-230">When you click the 360 Online tile in the Access Panel, you should get automatically signed-on to your 360 Online application.</span><span class="sxs-lookup"><span data-stu-id="01c16-230">When you click the 360 Online tile in the Access Panel, you should get automatically signed-on to your 360 Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="01c16-231">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="01c16-231">Additional Resources</span></span>
* [<span data-ttu-id="01c16-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="01c16-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="01c16-233">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="01c16-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/tutorial_general_04.png

[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/tutorial_general_07.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/tutorial_general_08.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/tutorial_general_09.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/tutorial_general_203.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-360online-tutorial/tutorial_general_205.png


























