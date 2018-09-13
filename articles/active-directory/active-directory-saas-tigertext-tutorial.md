---
title: 'Tutorial: Azure Active Directory integration with TigerText Secure Messenger | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and TigerText Secure Messenger.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 03f1e128-5bcb-4e49-b6a3-fe22eedc6d5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: b0fee2cfdb3f44f77b55c506e738d0b4820568bd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661867"
---
# <a name="tutorial-azure-active-directory-integration-with-tigertext-secure-messenger"></a><span data-ttu-id="93aa8-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="93aa8-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span></span>
<span data-ttu-id="93aa8-104">In this tutorial, you learn how to integrate TigerText with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="93aa8-104">In this tutorial, you learn how to integrate TigerText with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="93aa8-105">Integrating TigerText with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="93aa8-105">Integrating TigerText with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="93aa8-106">You can control in Azure AD who has access to TigerText</span><span class="sxs-lookup"><span data-stu-id="93aa8-106">You can control in Azure AD who has access to TigerText</span></span>
* <span data-ttu-id="93aa8-107">You can enable your users to automatically get signed-on to TigerText (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="93aa8-107">You can enable your users to automatically get signed-on to TigerText (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="93aa8-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="93aa8-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="93aa8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="93aa8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93aa8-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="93aa8-110">Prerequisites</span></span>
<span data-ttu-id="93aa8-111">To configure Azure AD integration with TigerText, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="93aa8-111">To configure Azure AD integration with TigerText, you need the following items:</span></span>

* <span data-ttu-id="93aa8-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="93aa8-112">An Azure AD subscription</span></span>
* <span data-ttu-id="93aa8-113">A TigerText single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="93aa8-113">A TigerText single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="93aa8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="93aa8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="93aa8-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="93aa8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="93aa8-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="93aa8-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="93aa8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="93aa8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="93aa8-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="93aa8-118">Scenario description</span></span>
<span data-ttu-id="93aa8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="93aa8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="93aa8-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="93aa8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="93aa8-121">Adding TigerText from the gallery</span><span class="sxs-lookup"><span data-stu-id="93aa8-121">Adding TigerText from the gallery</span></span>
2. <span data-ttu-id="93aa8-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="93aa8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tigertext-from-the-gallery"></a><span data-ttu-id="93aa8-123">Adding TigerText from the gallery</span><span class="sxs-lookup"><span data-stu-id="93aa8-123">Adding TigerText from the gallery</span></span>
<span data-ttu-id="93aa8-124">To configure the integration of TigerText into Azure AD, you need to add TigerText from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="93aa8-124">To configure the integration of TigerText into Azure AD, you need to add TigerText from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="93aa8-125">**To add TigerText from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="93aa8-125">**To add TigerText from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="93aa8-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="93aa8-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="93aa8-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="93aa8-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="93aa8-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="93aa8-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="93aa8-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="93aa8-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="93aa8-135">In the search box, type **TigerText**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-135">In the search box, type **TigerText**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_01.png)
7. <span data-ttu-id="93aa8-137">In the results pane, select **TigerText**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="93aa8-137">In the results pane, select **TigerText**, and then click **Complete** to add the application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="93aa8-138">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="93aa8-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="93aa8-139">In this section, you configure and test Azure AD single sign-on with TigerText based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="93aa8-139">In this section, you configure and test Azure AD single sign-on with TigerText based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="93aa8-140">For single sign-on to work, Azure AD needs to know what the counterpart user in TigerText is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93aa8-140">For single sign-on to work, Azure AD needs to know what the counterpart user in TigerText is to a user in Azure AD.</span></span> <span data-ttu-id="93aa8-141">In other words, a link relationship between an Azure AD user and the related user in TigerText needs to be established.</span><span class="sxs-lookup"><span data-stu-id="93aa8-141">In other words, a link relationship between an Azure AD user and the related user in TigerText needs to be established.</span></span>

<span data-ttu-id="93aa8-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in TigerText.</span><span class="sxs-lookup"><span data-stu-id="93aa8-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in TigerText.</span></span>

<span data-ttu-id="93aa8-143">To configure and test Azure AD single sign-on with TigerText, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="93aa8-143">To configure and test Azure AD single sign-on with TigerText, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="93aa8-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="93aa8-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="93aa8-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="93aa8-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="93aa8-146">**[Creating a TigerText test user](#creating-a-tigertext-test-user)** - to have a counterpart of Britta Simon in TigerText that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="93aa8-146">**[Creating a TigerText test user](#creating-a-tigertext-test-user)** - to have a counterpart of Britta Simon in TigerText that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="93aa8-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="93aa8-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="93aa8-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="93aa8-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="93aa8-149">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="93aa8-149">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="93aa8-150">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your TigerText application.</span><span class="sxs-lookup"><span data-stu-id="93aa8-150">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your TigerText application.</span></span>

<span data-ttu-id="93aa8-151">**To configure Azure AD single sign-on with TigerText, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="93aa8-151">**To configure Azure AD single sign-on with TigerText, perform the following steps:**</span></span>

1. <span data-ttu-id="93aa8-152">In the classic portal, on the **TigerText** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="93aa8-152">In the classic portal, on the **TigerText** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="93aa8-154">On the **How would you like users to sign on to TigerText** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-154">On the **How would you like users to sign on to TigerText** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_03.png) 
3. <span data-ttu-id="93aa8-156">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="93aa8-156">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_04.png) 
   
    <span data-ttu-id="93aa8-158">a.</span><span class="sxs-lookup"><span data-stu-id="93aa8-158">a.</span></span> <span data-ttu-id="93aa8-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your TigerText application using the following pattern: `https://<your-subdomain>.region.tigertext.com`.</span><span class="sxs-lookup"><span data-stu-id="93aa8-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your TigerText application using the following pattern: `https://<your-subdomain>.region.tigertext.com`.</span></span>
   
    <span data-ttu-id="93aa8-160">b.</span><span class="sxs-lookup"><span data-stu-id="93aa8-160">b.</span></span> <span data-ttu-id="93aa8-161">In the **Identifier** textbox, type a URL using the following pattern:`https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span><span class="sxs-lookup"><span data-stu-id="93aa8-161">In the **Identifier** textbox, type a URL using the following pattern:`https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span></span>
4. <span data-ttu-id="93aa8-162">On the **Configure single sign-on at TigerText** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="93aa8-162">On the **Configure single sign-on at TigerText** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_05.png)
   
    <span data-ttu-id="93aa8-164">a.</span><span class="sxs-lookup"><span data-stu-id="93aa8-164">a.</span></span> <span data-ttu-id="93aa8-165">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="93aa8-165">Click **Download metadata**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="93aa8-166">b.</span><span class="sxs-lookup"><span data-stu-id="93aa8-166">b.</span></span> <span data-ttu-id="93aa8-167">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-167">Click **Next**.</span></span>
5. <span data-ttu-id="93aa8-168">To get SSO configured for your application, contact TigerText support  team at [prosupport@tigertext.com](mailTo:prosupport@tigertext.com) and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="93aa8-168">To get SSO configured for your application, contact TigerText support  team at [prosupport@tigertext.com](mailTo:prosupport@tigertext.com) and provide them with the following:</span></span>
   
    <span data-ttu-id="93aa8-169">• The **Downloaded metadata**</span><span class="sxs-lookup"><span data-stu-id="93aa8-169">• The **Downloaded metadata**</span></span>
6. <span data-ttu-id="93aa8-170">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-170">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="93aa8-172">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-172">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="93aa8-174">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="93aa8-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="93aa8-175">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="93aa8-175">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="93aa8-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="93aa8-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="93aa8-178">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-178">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="93aa8-180">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="93aa8-180">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="93aa8-181">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-181">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="93aa8-183">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-183">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="93aa8-185">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="93aa8-185">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/create_aaduser_05.png)</span></span> 
   
    <span data-ttu-id="93aa8-186">a.</span><span class="sxs-lookup"><span data-stu-id="93aa8-186">a.</span></span> <span data-ttu-id="93aa8-187">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="93aa8-187">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="93aa8-188">b.</span><span class="sxs-lookup"><span data-stu-id="93aa8-188">b.</span></span> <span data-ttu-id="93aa8-189">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-189">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="93aa8-190">c.</span><span class="sxs-lookup"><span data-stu-id="93aa8-190">c.</span></span> <span data-ttu-id="93aa8-191">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-191">Click **Next**.</span></span>
6. <span data-ttu-id="93aa8-192">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="93aa8-192">On the **User Profile** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="93aa8-194">a.</span><span class="sxs-lookup"><span data-stu-id="93aa8-194">a.</span></span> <span data-ttu-id="93aa8-195">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-195">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="93aa8-196">b.</span><span class="sxs-lookup"><span data-stu-id="93aa8-196">b.</span></span> <span data-ttu-id="93aa8-197">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-197">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="93aa8-198">c.</span><span class="sxs-lookup"><span data-stu-id="93aa8-198">c.</span></span> <span data-ttu-id="93aa8-199">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-199">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="93aa8-200">d.</span><span class="sxs-lookup"><span data-stu-id="93aa8-200">d.</span></span> <span data-ttu-id="93aa8-201">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-201">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="93aa8-202">e.</span><span class="sxs-lookup"><span data-stu-id="93aa8-202">e.</span></span> <span data-ttu-id="93aa8-203">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-203">Click **Next**.</span></span>

7. <span data-ttu-id="93aa8-204">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-204">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="93aa8-206">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="93aa8-206">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="93aa8-208">a.</span><span class="sxs-lookup"><span data-stu-id="93aa8-208">a.</span></span> <span data-ttu-id="93aa8-209">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-209">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="93aa8-210">b.</span><span class="sxs-lookup"><span data-stu-id="93aa8-210">b.</span></span> <span data-ttu-id="93aa8-211">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-211">Click **Complete**.</span></span>   

### <a name="creating-an-tigertext-test-user"></a><span data-ttu-id="93aa8-212">Creating an TigerText test user</span><span class="sxs-lookup"><span data-stu-id="93aa8-212">Creating an TigerText test user</span></span>
<span data-ttu-id="93aa8-213">In this section, you create a user called Britta Simon in TigerText.</span><span class="sxs-lookup"><span data-stu-id="93aa8-213">In this section, you create a user called Britta Simon in TigerText.</span></span> <span data-ttu-id="93aa8-214">Please reach out to TigerText support team at [prosupport@tigertext.com](mailTo:prosupport@tigertext.com) to add the users in the TigerText platform.</span><span class="sxs-lookup"><span data-stu-id="93aa8-214">Please reach out to TigerText support team at [prosupport@tigertext.com](mailTo:prosupport@tigertext.com) to add the users in the TigerText platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="93aa8-215">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="93aa8-215">Assigning the Azure AD test user</span></span>
<span data-ttu-id="93aa8-216">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to TigerText.</span><span class="sxs-lookup"><span data-stu-id="93aa8-216">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to TigerText.</span></span>

![Assign User][200] 

<span data-ttu-id="93aa8-218">**To assign Britta Simon to TigerText, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="93aa8-218">**To assign Britta Simon to TigerText, perform the following steps:**</span></span>

1. <span data-ttu-id="93aa8-219">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="93aa8-219">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="93aa8-221">In the applications list, select **TigerText**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-221">In the applications list, select **TigerText**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_50.png) 
3. <span data-ttu-id="93aa8-223">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-223">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="93aa8-225">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-225">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="93aa8-226">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="93aa8-226">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="93aa8-228">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="93aa8-228">Testing Single Sign-On</span></span>
<span data-ttu-id="93aa8-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="93aa8-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="93aa8-230">When you click the TigerText tile in the Access Panel, you should get automatically signed-on to your TigerText application.</span><span class="sxs-lookup"><span data-stu-id="93aa8-230">When you click the TigerText tile in the Access Panel, you should get automatically signed-on to your TigerText application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="93aa8-231">Additional resources</span><span class="sxs-lookup"><span data-stu-id="93aa8-231">Additional resources</span></span>
* [<span data-ttu-id="93aa8-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="93aa8-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="93aa8-233">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="93aa8-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tigertext-tutorial/tutorial_general_205.png
























