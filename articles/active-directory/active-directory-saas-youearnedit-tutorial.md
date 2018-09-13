---
title: 'Tutorial: Azure Active Directory integration with YouEarnedIt | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and YouEarnedIt.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 3011d44d-dfcf-4061-888f-cff90fbc8150
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2017
ms.author: jeedes
ms.openlocfilehash: 1dcf3e5b71abeb13ed17554ac31cc20e765b4205
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662670"
---
# <a name="tutorial-azure-active-directory-integration-with-youearnedit"></a><span data-ttu-id="96d65-103">Tutorial: Azure Active Directory integration with YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="96d65-103">Tutorial: Azure Active Directory integration with YouEarnedIt</span></span>
<span data-ttu-id="96d65-104">In this tutorial, you learn how to integrate YouEarnedIt with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="96d65-104">In this tutorial, you learn how to integrate YouEarnedIt with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="96d65-105">Integrating YouEarnedIt with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="96d65-105">Integrating YouEarnedIt with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="96d65-106">You can control in Azure AD who has access to YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="96d65-106">You can control in Azure AD who has access to YouEarnedIt</span></span>
* <span data-ttu-id="96d65-107">You can enable your users to automatically get signed-on to YouEarnedIt single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="96d65-107">You can enable your users to automatically get signed-on to YouEarnedIt single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="96d65-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="96d65-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="96d65-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="96d65-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96d65-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="96d65-110">Prerequisites</span></span>
<span data-ttu-id="96d65-111">To configure Azure AD integration with YouEarnedIt, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="96d65-111">To configure Azure AD integration with YouEarnedIt, you need the following items:</span></span>

* <span data-ttu-id="96d65-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="96d65-112">An Azure AD subscription</span></span>
* <span data-ttu-id="96d65-113">A YouEarnedIt single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="96d65-113">A YouEarnedIt single-sign on enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="96d65-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="96d65-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="96d65-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="96d65-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="96d65-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="96d65-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="96d65-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="96d65-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="96d65-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="96d65-118">Scenario Description</span></span>
<span data-ttu-id="96d65-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="96d65-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="96d65-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="96d65-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="96d65-121">Adding YouEarnedIt from the gallery</span><span class="sxs-lookup"><span data-stu-id="96d65-121">Adding YouEarnedIt from the gallery</span></span>
2. <span data-ttu-id="96d65-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="96d65-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-youearnedit-from-the-gallery"></a><span data-ttu-id="96d65-123">Add YouEarnedIt from the gallery</span><span class="sxs-lookup"><span data-stu-id="96d65-123">Add YouEarnedIt from the gallery</span></span>
<span data-ttu-id="96d65-124">To configure the integration of YouEarnedIt into Azure AD, you need to add YouEarnedIt from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="96d65-124">To configure the integration of YouEarnedIt into Azure AD, you need to add YouEarnedIt from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="96d65-125">**To add YouEarnedIt from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="96d65-125">**To add YouEarnedIt from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="96d65-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="96d65-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="96d65-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="96d65-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="96d65-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="96d65-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="96d65-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="96d65-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="96d65-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="96d65-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="96d65-135">In the search box, type **YouEarnedIt**.</span><span class="sxs-lookup"><span data-stu-id="96d65-135">In the search box, type **YouEarnedIt**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_01.png)
7. <span data-ttu-id="96d65-137">In the results pane, select **YouEarnedIt**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="96d65-137">In the results pane, select **YouEarnedIt**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_06.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="96d65-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="96d65-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="96d65-140">In this section, you configure and test Azure AD single sign-on with YouEarnedIt based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="96d65-140">In this section, you configure and test Azure AD single sign-on with YouEarnedIt based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="96d65-141">For single sign-on to work, Azure AD needs to know what the counterpart user in YouEarnedIt is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="96d65-141">For single sign-on to work, Azure AD needs to know what the counterpart user in YouEarnedIt is to a user in Azure AD.</span></span> <span data-ttu-id="96d65-142">In other words, a link relationship between an Azure AD user and the related user in YouEarnedIt needs to be established.</span><span class="sxs-lookup"><span data-stu-id="96d65-142">In other words, a link relationship between an Azure AD user and the related user in YouEarnedIt needs to be established.</span></span>

<span data-ttu-id="96d65-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="96d65-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in YouEarnedIt.</span></span>

<span data-ttu-id="96d65-144">To configure and test Azure AD single sign-on with YouEarnedIt, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="96d65-144">To configure and test Azure AD single sign-on with YouEarnedIt, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="96d65-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="96d65-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="96d65-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="96d65-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="96d65-147">**[Creating a YouEarnedIt test user](#creating-a-predictix-price-reporting-test-user)** - to have a counterpart of Britta Simon in YouEarnedIt that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="96d65-147">**[Creating a YouEarnedIt test user](#creating-a-predictix-price-reporting-test-user)** - to have a counterpart of Britta Simon in YouEarnedIt that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="96d65-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="96d65-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="96d65-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="96d65-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="96d65-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="96d65-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="96d65-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your YouEarnedIt application.</span><span class="sxs-lookup"><span data-stu-id="96d65-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your YouEarnedIt application.</span></span>

<span data-ttu-id="96d65-152">**To configure Azure AD single sign-on with YouEarnedIt, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="96d65-152">**To configure Azure AD single sign-on with YouEarnedIt, perform the following steps:**</span></span>

1. <span data-ttu-id="96d65-153">In the classic portal, on the **YouEarnedIt** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="96d65-153">In the classic portal, on the **YouEarnedIt** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="96d65-155">On the **How would you like users to sign on to YouEarnedIt** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="96d65-155">On the **How would you like users to sign on to YouEarnedIt** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_03.png) 
3. <span data-ttu-id="96d65-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="96d65-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_04.png) 
  1. <span data-ttu-id="96d65-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your YouEarnedIt application using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="96d65-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your YouEarnedIt application using the following pattern:</span></span>  
    * <span data-ttu-id="96d65-160">Sandbox environment: `https://<company name>.sandbox.youearnedit.com/users/sign_in`</span><span class="sxs-lookup"><span data-stu-id="96d65-160">Sandbox environment: `https://<company name>.sandbox.youearnedit.com/users/sign_in`</span></span>
    * <span data-ttu-id="96d65-161">Production environment: `https://<company name>.youearnedit.com/users/sign_in`</span><span class="sxs-lookup"><span data-stu-id="96d65-161">Production environment: `https://<company name>.youearnedit.com/users/sign_in`</span></span>  
   2. <span data-ttu-id="96d65-162">click **Next**</span><span class="sxs-lookup"><span data-stu-id="96d65-162">click **Next**</span></span>
4. <span data-ttu-id="96d65-163">On the **Configure single sign-on at YouEarnedIt** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="96d65-163">On the **Configure single sign-on at YouEarnedIt** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_05.png)
  1. <span data-ttu-id="96d65-165">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="96d65-165">Click **Download certificate**, and then save the file on your computer.</span></span>  
  2. <span data-ttu-id="96d65-166">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="96d65-166">Click **Next**.</span></span>
5. <span data-ttu-id="96d65-167">To get SSO configured for your application, contact YouEarnedIt support team and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="96d65-167">To get SSO configured for your application, contact YouEarnedIt support team and provide them with the following:</span></span>  
    <span data-ttu-id="96d65-168">• The downloaded **certificate** • The **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="96d65-168">• The downloaded **certificate** • The **SAML SSO URL**</span></span>
6. <span data-ttu-id="96d65-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="96d65-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="96d65-171">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="96d65-171">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="96d65-173">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="96d65-173">Create an Azure AD test user</span></span>
<span data-ttu-id="96d65-174">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="96d65-174">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="96d65-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="96d65-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="96d65-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="96d65-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="96d65-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="96d65-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="96d65-180">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="96d65-180">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="96d65-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="96d65-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="96d65-184">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="96d65-184">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/create_aaduser_05.png)  
  1. <span data-ttu-id="96d65-186">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="96d65-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="96d65-187">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="96d65-187">In the User Name **textbox**, type **BrittaSimon**.</span></span>  
  3. <span data-ttu-id="96d65-188">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="96d65-188">Click **Next**.</span></span>
6. <span data-ttu-id="96d65-189">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="96d65-189">On the **User Profile** dialog page, perform the following steps:</span></span>

   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/create_aaduser_06.png)    
  1. <span data-ttu-id="96d65-191">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="96d65-191">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="96d65-192">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="96d65-192">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="96d65-193">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="96d65-193">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="96d65-194">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="96d65-194">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="96d65-195">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="96d65-195">Click **Next**.</span></span>
7. <span data-ttu-id="96d65-196">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="96d65-196">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="96d65-198">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="96d65-198">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="96d65-200">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="96d65-200">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="96d65-201">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="96d65-201">Click **Complete**.</span></span>   

### <a name="create-an-youearnedit-test-user"></a><span data-ttu-id="96d65-202">Create an YouEarnedIt test user</span><span class="sxs-lookup"><span data-stu-id="96d65-202">Create an YouEarnedIt test user</span></span>
<span data-ttu-id="96d65-203">In this section, you create a user called Britta Simon in YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="96d65-203">In this section, you create a user called Britta Simon in YouEarnedIt.</span></span> <span data-ttu-id="96d65-204">Please work with YouEarnedIt support team to add the users in the YouEarnedIt platform.</span><span class="sxs-lookup"><span data-stu-id="96d65-204">Please work with YouEarnedIt support team to add the users in the YouEarnedIt platform.</span></span>

>[!NOTE]
><span data-ttu-id="96d65-205">YouEarnedIt expect the Identity Provider to supply an EmailAddress  or UserName in the NameID attribute.</span><span class="sxs-lookup"><span data-stu-id="96d65-205">YouEarnedIt expect the Identity Provider to supply an EmailAddress  or UserName in the NameID attribute.</span></span> <span data-ttu-id="96d65-206">Authentication will fail if a corresponding UserName or EmailAddress is not found within the database or does not match exactly.</span><span class="sxs-lookup"><span data-stu-id="96d65-206">Authentication will fail if a corresponding UserName or EmailAddress is not found within the database or does not match exactly.</span></span> <span data-ttu-id="96d65-207">This will require that accounts be imported into the YouEarnedIt system before the SSO integration (Typically either via API or CSV import).</span><span class="sxs-lookup"><span data-stu-id="96d65-207">This will require that accounts be imported into the YouEarnedIt system before the SSO integration (Typically either via API or CSV import).</span></span>
>  

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="96d65-208">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="96d65-208">Assign the Azure AD test user</span></span>
<span data-ttu-id="96d65-209">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="96d65-209">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to YouEarnedIt.</span></span>

![Assign User][200] 

<span data-ttu-id="96d65-211">**To assign Britta Simon to YouEarnedIt, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="96d65-211">**To assign Britta Simon to YouEarnedIt, perform the following steps:**</span></span>

1. <span data-ttu-id="96d65-212">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="96d65-212">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="96d65-214">In the applications list, select **YouEarnedIt**.</span><span class="sxs-lookup"><span data-stu-id="96d65-214">In the applications list, select **YouEarnedIt**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_50.png) 
3. <span data-ttu-id="96d65-216">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="96d65-216">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="96d65-218">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="96d65-218">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="96d65-219">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="96d65-219">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="96d65-221">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="96d65-221">Test single sign-on</span></span>
<span data-ttu-id="96d65-222">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="96d65-222">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="96d65-223">When you click the YouEarnedIt tile in the Access Panel, you should get automatically signed-on to your YouEarnedIt application.</span><span class="sxs-lookup"><span data-stu-id="96d65-223">When you click the YouEarnedIt tile in the Access Panel, you should get automatically signed-on to your YouEarnedIt application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="96d65-224">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="96d65-224">Additional Resources</span></span>
* [<span data-ttu-id="96d65-225">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96d65-225">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="96d65-226">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="96d65-226">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-youearnedit-tutorial/tutorial_general_205.png

























