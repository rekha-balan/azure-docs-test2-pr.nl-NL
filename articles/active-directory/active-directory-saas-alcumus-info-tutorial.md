---
title: 'Tutorial: Azure Active Directory integration with Alcumus Info Exchange | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Alcumus Info Exchange.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: d26034b8-f0d5-4f65-aa56-0fc168ceec8c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 1706601924e83f1a76f7e08657ddb60f37b0d806
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662290"
---
# <a name="tutorial-azure-active-directory-integration-with-alcumus-info-exchange"></a><span data-ttu-id="aacea-103">Tutorial: Azure Active Directory integration with Alcumus Info Exchange</span><span class="sxs-lookup"><span data-stu-id="aacea-103">Tutorial: Azure Active Directory integration with Alcumus Info Exchange</span></span>
<span data-ttu-id="aacea-104">The objective of this tutorial is to show you how to integrate Alcumus Info Exchange with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="aacea-104">The objective of this tutorial is to show you how to integrate Alcumus Info Exchange with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="aacea-105">Integrating Alcumus Info Exchange with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="aacea-105">Integrating Alcumus Info Exchange with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="aacea-106">You can control in Azure AD who has access to Alcumus Info Exchange</span><span class="sxs-lookup"><span data-stu-id="aacea-106">You can control in Azure AD who has access to Alcumus Info Exchange</span></span> 
* <span data-ttu-id="aacea-107">You can enable your users to automatically get signed-on to Alcumus Info Exchange (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="aacea-107">You can enable your users to automatically get signed-on to Alcumus Info Exchange (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="aacea-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="aacea-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="aacea-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aacea-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aacea-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="aacea-110">Prerequisites</span></span>
<span data-ttu-id="aacea-111">To configure Azure AD integration with Alcumus Info Exchange, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="aacea-111">To configure Azure AD integration with Alcumus Info Exchange, you need the following items:</span></span>

* <span data-ttu-id="aacea-112">An [Azure AD](https://azure.microsoft.com/) subscription</span><span class="sxs-lookup"><span data-stu-id="aacea-112">An [Azure AD](https://azure.microsoft.com/) subscription</span></span>
* <span data-ttu-id="aacea-113">An [Alcumus Info Exchange](http://www.alcumusgroup.com/) single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="aacea-113">An [Alcumus Info Exchange](http://www.alcumusgroup.com/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aacea-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="aacea-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="aacea-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="aacea-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="aacea-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="aacea-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="aacea-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aacea-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="aacea-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="aacea-118">Scenario Description</span></span>
<span data-ttu-id="aacea-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="aacea-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="aacea-120">The scenario outlined in this tutorial consists of three main building blocks:</span><span class="sxs-lookup"><span data-stu-id="aacea-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="aacea-121">Adding Alcumus Info Exchange from the gallery</span><span class="sxs-lookup"><span data-stu-id="aacea-121">Adding Alcumus Info Exchange from the gallery</span></span> 
2. <span data-ttu-id="aacea-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="aacea-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-alcumus-info-exchange-from-the-gallery"></a><span data-ttu-id="aacea-123">Adding Alcumus Info Exchange from the gallery</span><span class="sxs-lookup"><span data-stu-id="aacea-123">Adding Alcumus Info Exchange from the gallery</span></span>
<span data-ttu-id="aacea-124">To configure the integration of Alcumus Info Exchange into Azure AD, you need to add Alcumus Info Exchange from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="aacea-124">To configure the integration of Alcumus Info Exchange into Azure AD, you need to add Alcumus Info Exchange from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="aacea-125">**To add Alcumus Info Exchange from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="aacea-125">**To add Alcumus Info Exchange from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="aacea-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aacea-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="aacea-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="aacea-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="aacea-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="aacea-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="aacea-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="aacea-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="aacea-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="aacea-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="aacea-135">In the search box, type **Alcumus Info Exchange**.</span><span class="sxs-lookup"><span data-stu-id="aacea-135">In the search box, type **Alcumus Info Exchange**.</span></span>
   
    ![Applications][5]
7. <span data-ttu-id="aacea-137">In the results pane, select **Alcumus Info Exchange**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="aacea-137">In the results pane, select **Alcumus Info Exchange**, and then click **Complete** to add the application.</span></span>
   
    ![Applications][400]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aacea-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="aacea-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="aacea-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Alcumus Info Exchange based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="aacea-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Alcumus Info Exchange based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="aacea-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Alcumus Info Exchange to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="aacea-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Alcumus Info Exchange to an user in Azure AD is.</span></span> <span data-ttu-id="aacea-142">In other words, a link relationship between an Azure AD user and the related user in Alcumus Info Exchange needs to be established.</span><span class="sxs-lookup"><span data-stu-id="aacea-142">In other words, a link relationship between an Azure AD user and the related user in Alcumus Info Exchange needs to be established.</span></span>  
<span data-ttu-id="aacea-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="aacea-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Alcumus Info Exchange.</span></span>

<span data-ttu-id="aacea-144">To configure and test Azure AD single sign-on with Alcumus Info Exchange, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="aacea-144">To configure and test Azure AD single sign-on with Alcumus Info Exchange, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="aacea-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="aacea-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="aacea-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aacea-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aacea-147">**[Creating a Alcumus Info Exchange test user](#creating-a-alcumus-info-exchange-test-user)** - to have a counterpart of Britta Simon in Alcumus Info Exchange that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="aacea-147">**[Creating a Alcumus Info Exchange test user](#creating-a-alcumus-info-exchange-test-user)** - to have a counterpart of Britta Simon in Alcumus Info Exchange that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="aacea-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="aacea-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aacea-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="aacea-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aacea-150">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="aacea-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="aacea-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Alcumus Info Exchange application.</span><span class="sxs-lookup"><span data-stu-id="aacea-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Alcumus Info Exchange application.</span></span>

<span data-ttu-id="aacea-152">**To configure Azure AD single sign-on with Alcumus Info Exchange, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="aacea-152">**To configure Azure AD single sign-on with Alcumus Info Exchange, perform the following steps:**</span></span>

1. <span data-ttu-id="aacea-153">In the Azure classic portal, on the **Alcumus Info Exchange** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="aacea-153">In the Azure classic portal, on the **Alcumus Info Exchange** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6]
2. <span data-ttu-id="aacea-155">On the **How would you like users to sign on to Alcumus Info Exchange** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="aacea-155">On the **How would you like users to sign on to Alcumus Info Exchange** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][7]
3. <span data-ttu-id="aacea-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="aacea-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![Azure AD Single Sign-On][8]
   
    <span data-ttu-id="aacea-159">a.</span><span class="sxs-lookup"><span data-stu-id="aacea-159">a.</span></span> <span data-ttu-id="aacea-160">in the **Reply URL** textbox, type the consumer URL that was setup for you by your Alcumus Info Exchange support team.</span><span class="sxs-lookup"><span data-stu-id="aacea-160">in the **Reply URL** textbox, type the consumer URL that was setup for you by your Alcumus Info Exchange support team.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="aacea-161">If you don't know what the right value is, contact the Alcumus Info Exchange support team via [helpdesk@alcumusgroup.com](mailto:helpdesk@alcumusgroup.com).</span><span class="sxs-lookup"><span data-stu-id="aacea-161">If you don't know what the right value is, contact the Alcumus Info Exchange support team via [helpdesk@alcumusgroup.com](mailto:helpdesk@alcumusgroup.com).</span></span>
   > 
   > 
   
    <span data-ttu-id="aacea-162">b.</span><span class="sxs-lookup"><span data-stu-id="aacea-162">b.</span></span> <span data-ttu-id="aacea-163">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="aacea-163">Click **Next**.</span></span>
4. <span data-ttu-id="aacea-164">On the **Configure single sign-on at Alcumus Info Exchange** page, click **Download metadata**, and then save the metadata file locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="aacea-164">On the **Configure single sign-on at Alcumus Info Exchange** page, click **Download metadata**, and then save the metadata file locally on your computer.</span></span>
   
    ![What is Azure AD Connect][9]
5. <span data-ttu-id="aacea-166">Contact the Alcumus Info Exchange support team via [helpdesk@alcumusgroup.com](mailto:helpdesk@alcumusgroup.com), provide them with the metadata file, and them let them know that they should enable SSO for you.</span><span class="sxs-lookup"><span data-stu-id="aacea-166">Contact the Alcumus Info Exchange support team via [helpdesk@alcumusgroup.com](mailto:helpdesk@alcumusgroup.com), provide them with the metadata file, and them let them know that they should enable SSO for you.</span></span>
6. <span data-ttu-id="aacea-167">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="aacea-167">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![What is Azure AD Connect][10]
7. <span data-ttu-id="aacea-169">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="aacea-169">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![What is Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aacea-171">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="aacea-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="aacea-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aacea-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Create Azure AD User][20]

<span data-ttu-id="aacea-174">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="aacea-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="aacea-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="aacea-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="aacea-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="aacea-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="aacea-178">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="aacea-178">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="aacea-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="aacea-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="aacea-182">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="aacea-182">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="aacea-184">a.</span><span class="sxs-lookup"><span data-stu-id="aacea-184">a.</span></span> <span data-ttu-id="aacea-185">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="aacea-185">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="aacea-186">b.</span><span class="sxs-lookup"><span data-stu-id="aacea-186">b.</span></span> <span data-ttu-id="aacea-187">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="aacea-187">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="aacea-188">c.</span><span class="sxs-lookup"><span data-stu-id="aacea-188">c.</span></span> <span data-ttu-id="aacea-189">Click Next.</span><span class="sxs-lookup"><span data-stu-id="aacea-189">Click Next.</span></span>
6. <span data-ttu-id="aacea-190">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="aacea-190">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="aacea-192">a.</span><span class="sxs-lookup"><span data-stu-id="aacea-192">a.</span></span> <span data-ttu-id="aacea-193">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="aacea-193">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="aacea-194">b.</span><span class="sxs-lookup"><span data-stu-id="aacea-194">b.</span></span> <span data-ttu-id="aacea-195">In the **Last Name** txtbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="aacea-195">In the **Last Name** txtbox, type, **Simon**.</span></span>

    <span data-ttu-id="aacea-196">c.</span><span class="sxs-lookup"><span data-stu-id="aacea-196">c.</span></span> <span data-ttu-id="aacea-197">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="aacea-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="aacea-198">d.</span><span class="sxs-lookup"><span data-stu-id="aacea-198">d.</span></span> <span data-ttu-id="aacea-199">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="aacea-199">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="aacea-200">e.</span><span class="sxs-lookup"><span data-stu-id="aacea-200">e.</span></span> <span data-ttu-id="aacea-201">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="aacea-201">Click **Next**.</span></span>


1. <span data-ttu-id="aacea-202">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="aacea-202">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/create_aaduser_07.png) 
2. <span data-ttu-id="aacea-204">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="aacea-204">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="aacea-206">a.</span><span class="sxs-lookup"><span data-stu-id="aacea-206">a.</span></span> <span data-ttu-id="aacea-207">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="aacea-207">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="aacea-208">b.</span><span class="sxs-lookup"><span data-stu-id="aacea-208">b.</span></span> <span data-ttu-id="aacea-209">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="aacea-209">Click **Complete**.</span></span>   

### <a name="creating-a-alcumus-info-exchange-test-user"></a><span data-ttu-id="aacea-210">Creating a Alcumus Info Exchange test user</span><span class="sxs-lookup"><span data-stu-id="aacea-210">Creating a Alcumus Info Exchange test user</span></span>
<span data-ttu-id="aacea-211">The objective of this section is to create a user called Britta Simon in Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="aacea-211">The objective of this section is to create a user called Britta Simon in Alcumus Info Exchange.</span></span>

<span data-ttu-id="aacea-212">**To create a user called Britta Simon in Alcumus Info Exchange, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="aacea-212">**To create a user called Britta Simon in Alcumus Info Exchange, perform the following steps:**</span></span>

1. <span data-ttu-id="aacea-213">Contact the Alcumus Info Exchange support team via [helpdesk@alcumusgroup.com](mailto:helpdesk@alcumusgroup.com),</span><span class="sxs-lookup"><span data-stu-id="aacea-213">Contact the Alcumus Info Exchange support team via [helpdesk@alcumusgroup.com](mailto:helpdesk@alcumusgroup.com),</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="aacea-214">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="aacea-214">Assigning the Azure AD test user</span></span>
<span data-ttu-id="aacea-215">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="aacea-215">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Alcumus Info Exchange.</span></span>

![Assign User][200]

<span data-ttu-id="aacea-217">**To assign Britta Simon to Alcumus Info Exchange, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="aacea-217">**To assign Britta Simon to Alcumus Info Exchange, perform the following steps:**</span></span>

1. <span data-ttu-id="aacea-218">On the Azure portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="aacea-218">On the Azure portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201]
2. <span data-ttu-id="aacea-220">In the applications list, select **Alcumus Info Exchange**.</span><span class="sxs-lookup"><span data-stu-id="aacea-220">In the applications list, select **Alcumus Info Exchange**.</span></span>
   
    ![Assign User][202]
3. <span data-ttu-id="aacea-222">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="aacea-222">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="aacea-224">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="aacea-224">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="aacea-225">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="aacea-225">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="aacea-227">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="aacea-227">Testing Single Sign-On</span></span>
<span data-ttu-id="aacea-228">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="aacea-228">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="aacea-229">When you click the Alcumus Info Exchange tile in the Access Panel, you should get automatically signed-on to your Alcumus Info Exchange application.</span><span class="sxs-lookup"><span data-stu-id="aacea-229">When you click the Alcumus Info Exchange tile in the Access Panel, you should get automatically signed-on to your Alcumus Info Exchange application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="aacea-230">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="aacea-230">Additional Resources</span></span>
* [<span data-ttu-id="aacea-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="aacea-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aacea-232">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="aacea-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/tutorial_general_04.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumus_01.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumus_02.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumus_03.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumus_04.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumus_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumus_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumus_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumus_08.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/tutorial_general_205.png
[400]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumus_402.png

























