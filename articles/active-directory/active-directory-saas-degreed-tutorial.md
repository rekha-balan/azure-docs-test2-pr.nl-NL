---
title: 'Tutorial: Azure Active Directory integration with Asset Bank | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Asset Bank.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 1eda2d1c-b5e2-4c53-ad46-bbeb91cd119a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 633cad0bd95e315b146cdddf6c24296593621fdb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550590"
---
# <a name="tutorial-azure-active-directory-integration-with-degreed"></a><span data-ttu-id="dea8f-103">Tutorial: Azure Active Directory integration with Degreed</span><span class="sxs-lookup"><span data-stu-id="dea8f-103">Tutorial: Azure Active Directory integration with Degreed</span></span>
<span data-ttu-id="dea8f-104">The objective of this tutorial is to show you how to integrate Degreed with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dea8f-104">The objective of this tutorial is to show you how to integrate Degreed with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="dea8f-105">Integrating Degreed with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="dea8f-105">Integrating Degreed with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="dea8f-106">You can control in Azure AD who has access to Degreed</span><span class="sxs-lookup"><span data-stu-id="dea8f-106">You can control in Azure AD who has access to Degreed</span></span>
* <span data-ttu-id="dea8f-107">You can enable your users to automatically get signed-on to Degreed (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="dea8f-107">You can enable your users to automatically get signed-on to Degreed (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="dea8f-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="dea8f-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="dea8f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dea8f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dea8f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dea8f-110">Prerequisites</span></span>
<span data-ttu-id="dea8f-111">To configure Azure AD integration with Degreed, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="dea8f-111">To configure Azure AD integration with Degreed, you need the following items:</span></span>

* <span data-ttu-id="dea8f-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="dea8f-112">An Azure AD subscription</span></span>
* <span data-ttu-id="dea8f-113">A Degreed single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="dea8f-113">A Degreed single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dea8f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="dea8f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="dea8f-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="dea8f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="dea8f-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="dea8f-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="dea8f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dea8f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dea8f-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="dea8f-118">Scenario Description</span></span>
<span data-ttu-id="dea8f-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="dea8f-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="dea8f-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="dea8f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dea8f-121">Adding Degreed from the gallery</span><span class="sxs-lookup"><span data-stu-id="dea8f-121">Adding Degreed from the gallery</span></span>
2. <span data-ttu-id="dea8f-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dea8f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-degreed-from-the-gallery"></a><span data-ttu-id="dea8f-123">Adding Degreed from the gallery</span><span class="sxs-lookup"><span data-stu-id="dea8f-123">Adding Degreed from the gallery</span></span>
<span data-ttu-id="dea8f-124">To configure the integration of Degreed into Azure AD, you need to add Degreed from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="dea8f-124">To configure the integration of Degreed into Azure AD, you need to add Degreed from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dea8f-125">**To add Degreed from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dea8f-125">**To add Degreed from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dea8f-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="dea8f-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="dea8f-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="dea8f-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="dea8f-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="dea8f-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="dea8f-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="dea8f-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="dea8f-135">In the search box, type **Degreed**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-135">In the search box, type **Degreed**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/tutorial_degreed_01.png)
7. <span data-ttu-id="dea8f-137">In the results pane, select **Degreed**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="dea8f-137">In the results pane, select **Degreed**, and then click **Complete** to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/tutorial_degreed_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dea8f-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="dea8f-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dea8f-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Degreed based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="dea8f-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Degreed based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dea8f-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Degreed to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="dea8f-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Degreed to an user in Azure AD is.</span></span> <span data-ttu-id="dea8f-142">In other words, a link relationship between an Azure AD user and the related user in Degreed needs to be established.</span><span class="sxs-lookup"><span data-stu-id="dea8f-142">In other words, a link relationship between an Azure AD user and the related user in Degreed needs to be established.</span></span>

<span data-ttu-id="dea8f-143">To configure and test Azure AD single sign-on with Degreed, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="dea8f-143">To configure and test Azure AD single sign-on with Degreed, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dea8f-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="dea8f-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dea8f-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dea8f-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dea8f-146">**[Creating a Degreed test user](#creating-a-degreed-test-user)** - to have a counterpart of Britta Simon in Degreed that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="dea8f-146">**[Creating a Degreed test user](#creating-a-degreed-test-user)** - to have a counterpart of Britta Simon in Degreed that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="dea8f-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="dea8f-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dea8f-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="dea8f-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dea8f-149">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="dea8f-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="dea8f-150">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Degreed application.</span><span class="sxs-lookup"><span data-stu-id="dea8f-150">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Degreed application.</span></span>

<span data-ttu-id="dea8f-151">**To configure Azure AD single sign-on with Degreed, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dea8f-151">**To configure Azure AD single sign-on with Degreed, perform the following steps:**</span></span>

1. <span data-ttu-id="dea8f-152">In the Azure classic portal, on the **Degreed** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="dea8f-152">In the Azure classic portal, on the **Degreed** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="dea8f-154">On the **How would you like users to sign on to Degreed** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-154">On the **How would you like users to sign on to Degreed** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/tutorial_degreed_03.png) 
3. <span data-ttu-id="dea8f-156">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dea8f-156">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/tutorial_degreed_04.png) 

    <span data-ttu-id="dea8f-158">a.</span><span class="sxs-lookup"><span data-stu-id="dea8f-158">a.</span></span> <span data-ttu-id="dea8f-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your Degreed application using the following pattern: `https://degreed.com/?orgsso=<company code>`</span><span class="sxs-lookup"><span data-stu-id="dea8f-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your Degreed application using the following pattern: `https://degreed.com/?orgsso=<company code>`</span></span>

    <span data-ttu-id="dea8f-160">b.</span><span class="sxs-lookup"><span data-stu-id="dea8f-160">b.</span></span> <span data-ttu-id="dea8f-161">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-161">Click **Next**.</span></span>


1. <span data-ttu-id="dea8f-162">On the **Configure single sign-on at Degreed** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dea8f-162">On the **Configure single sign-on at Degreed** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/tutorial_degreed_05.png) 
   
    <span data-ttu-id="dea8f-164">a.</span><span class="sxs-lookup"><span data-stu-id="dea8f-164">a.</span></span> <span data-ttu-id="dea8f-165">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="dea8f-165">Click **Download metadata**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="dea8f-166">b.</span><span class="sxs-lookup"><span data-stu-id="dea8f-166">b.</span></span> <span data-ttu-id="dea8f-167">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-167">Click **Next**.</span></span>
2. <span data-ttu-id="dea8f-168">To get SSO configured for your application, contact your Degreed support team via [admin@degreed.com](mailto:admin@degreed.com) and attach the metadata file to your email.</span><span class="sxs-lookup"><span data-stu-id="dea8f-168">To get SSO configured for your application, contact your Degreed support team via [admin@degreed.com](mailto:admin@degreed.com) and attach the metadata file to your email.</span></span>
3. <span data-ttu-id="dea8f-169">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-169">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
4. <span data-ttu-id="dea8f-171">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-171">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dea8f-173">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="dea8f-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="dea8f-174">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dea8f-174">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="dea8f-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dea8f-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dea8f-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="dea8f-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="dea8f-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="dea8f-180">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-180">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="dea8f-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="dea8f-184">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dea8f-184">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="dea8f-186">a.</span><span class="sxs-lookup"><span data-stu-id="dea8f-186">a.</span></span> <span data-ttu-id="dea8f-187">As **Type Of User**, select **New user in your organization**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-187">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="dea8f-188">b.</span><span class="sxs-lookup"><span data-stu-id="dea8f-188">b.</span></span> <span data-ttu-id="dea8f-189">In the **User Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-189">In the **User Name** textbox, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="dea8f-190">c.</span><span class="sxs-lookup"><span data-stu-id="dea8f-190">c.</span></span> <span data-ttu-id="dea8f-191">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-191">Click **Next**.</span></span>
6. <span data-ttu-id="dea8f-192">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dea8f-192">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="dea8f-194">a.</span><span class="sxs-lookup"><span data-stu-id="dea8f-194">a.</span></span> <span data-ttu-id="dea8f-195">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-195">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="dea8f-196">b.</span><span class="sxs-lookup"><span data-stu-id="dea8f-196">b.</span></span> <span data-ttu-id="dea8f-197">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-197">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="dea8f-198">c.</span><span class="sxs-lookup"><span data-stu-id="dea8f-198">c.</span></span> <span data-ttu-id="dea8f-199">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-199">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="dea8f-200">d.</span><span class="sxs-lookup"><span data-stu-id="dea8f-200">d.</span></span> <span data-ttu-id="dea8f-201">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-201">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="dea8f-202">e.</span><span class="sxs-lookup"><span data-stu-id="dea8f-202">e.</span></span> <span data-ttu-id="dea8f-203">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-203">Click **Next**.</span></span>

7. <span data-ttu-id="dea8f-204">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-204">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="dea8f-206">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="dea8f-206">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="dea8f-208">a.</span><span class="sxs-lookup"><span data-stu-id="dea8f-208">a.</span></span> <span data-ttu-id="dea8f-209">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-209">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="dea8f-210">b.</span><span class="sxs-lookup"><span data-stu-id="dea8f-210">b.</span></span> <span data-ttu-id="dea8f-211">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-211">Click **Complete**.</span></span>   

### <a name="creating-a-degreed-test-user"></a><span data-ttu-id="dea8f-212">Creating a Degreed test user</span><span class="sxs-lookup"><span data-stu-id="dea8f-212">Creating a Degreed test user</span></span>
<span data-ttu-id="dea8f-213">The objective of this section is to create a user called Britta Simon in Degreed.</span><span class="sxs-lookup"><span data-stu-id="dea8f-213">The objective of this section is to create a user called Britta Simon in Degreed.</span></span> <span data-ttu-id="dea8f-214">Degreed supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="dea8f-214">Degreed supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="dea8f-215">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="dea8f-215">There is no action item for you in this section.</span></span> <span data-ttu-id="dea8f-216">A new user will be created during an attempt to access Degreed if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="dea8f-216">A new user will be created during an attempt to access Degreed if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="dea8f-217">If you need to create an user manually, you need to contact the Degreed support team.</span><span class="sxs-lookup"><span data-stu-id="dea8f-217">If you need to create an user manually, you need to contact the Degreed support team.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dea8f-218">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="dea8f-218">Assigning the Azure AD test user</span></span>
<span data-ttu-id="dea8f-219">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Degreed.</span><span class="sxs-lookup"><span data-stu-id="dea8f-219">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Degreed.</span></span>

![Assign User][200] 

<span data-ttu-id="dea8f-221">**To assign Britta Simon to Degreed, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="dea8f-221">**To assign Britta Simon to Degreed, perform the following steps:**</span></span>

1. <span data-ttu-id="dea8f-222">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="dea8f-222">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="dea8f-224">In the applications list, select **Degreed**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-224">In the applications list, select **Degreed**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/tutorial_degreed_50.png) 
3. <span data-ttu-id="dea8f-226">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-226">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="dea8f-228">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-228">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="dea8f-229">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="dea8f-229">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="dea8f-231">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="dea8f-231">Testing Single Sign-On</span></span>
<span data-ttu-id="dea8f-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="dea8f-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="dea8f-233">When you click the Degreed tile in the Access Panel, you should get automatically signed-on to your Degreed application.</span><span class="sxs-lookup"><span data-stu-id="dea8f-233">When you click the Degreed tile in the Access Panel, you should get automatically signed-on to your Degreed application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dea8f-234">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="dea8f-234">Additional Resources</span></span>
* [<span data-ttu-id="dea8f-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dea8f-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dea8f-236">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dea8f-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-degreed-tutorial/tutorial_general_205.png

























