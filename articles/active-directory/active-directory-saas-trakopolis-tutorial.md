---
title: 'Tutorial: Azure Active Directory integration with Trakopolis | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Trakopolis.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 73d67c3e-4b4b-4d3b-aa58-6699ea1ccea3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 9aafb35fda742373cd9dd061539f28ef5a26f1e2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553163"
---
# <a name="tutorial-azure-active-directory-integration-with-trakopolis"></a><span data-ttu-id="ff655-103">Tutorial: Azure Active Directory integration with Trakopolis</span><span class="sxs-lookup"><span data-stu-id="ff655-103">Tutorial: Azure Active Directory integration with Trakopolis</span></span>
<span data-ttu-id="ff655-104">The objective of this tutorial is to show you how to integrate Trakopolis with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ff655-104">The objective of this tutorial is to show you how to integrate Trakopolis with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="ff655-105">Integrating Trakopolis with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ff655-105">Integrating Trakopolis with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="ff655-106">You can control in Azure AD who has access to Trakopolis</span><span class="sxs-lookup"><span data-stu-id="ff655-106">You can control in Azure AD who has access to Trakopolis</span></span>
* <span data-ttu-id="ff655-107">You can enable your users to automatically get signed-on to Trakopolis (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="ff655-107">You can enable your users to automatically get signed-on to Trakopolis (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="ff655-108">You can manage your accounts in one central location - the Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff655-108">You can manage your accounts in one central location - the Azure Active Directory</span></span> 

<span data-ttu-id="ff655-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ff655-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff655-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ff655-110">Prerequisites</span></span>
<span data-ttu-id="ff655-111">To configure Azure AD integration with Trakopolis, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="ff655-111">To configure Azure AD integration with Trakopolis, you need the following items:</span></span>

* <span data-ttu-id="ff655-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="ff655-112">An Azure AD subscription</span></span>
* <span data-ttu-id="ff655-113">A Trakopolis single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ff655-113">A Trakopolis single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ff655-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="ff655-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="ff655-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="ff655-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="ff655-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="ff655-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="ff655-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff655-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ff655-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="ff655-118">Scenario Description</span></span>
<span data-ttu-id="ff655-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="ff655-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="ff655-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="ff655-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ff655-121">Adding Trakopolis from the gallery</span><span class="sxs-lookup"><span data-stu-id="ff655-121">Adding Trakopolis from the gallery</span></span>
2. <span data-ttu-id="ff655-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ff655-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trakopolis-from-the-gallery"></a><span data-ttu-id="ff655-123">Adding Trakopolis from the gallery</span><span class="sxs-lookup"><span data-stu-id="ff655-123">Adding Trakopolis from the gallery</span></span>
<span data-ttu-id="ff655-124">To configure the integration of Trakopolis into Azure AD, you need to add Trakopolis from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="ff655-124">To configure the integration of Trakopolis into Azure AD, you need to add Trakopolis from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ff655-125">**To add Trakopolis from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ff655-125">**To add Trakopolis from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ff655-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ff655-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="ff655-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="ff655-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="ff655-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="ff655-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="ff655-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="ff655-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="ff655-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="ff655-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="ff655-135">In the search box, type **Trakopolis**.</span><span class="sxs-lookup"><span data-stu-id="ff655-135">In the search box, type **Trakopolis**.</span></span>
   
    ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_01.png)

7. <span data-ttu-id="ff655-137">In the results pane, select **Trakopolis**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="ff655-137">In the results pane, select **Trakopolis**, and then click **Complete** to add the application.</span></span>
   
    ![Applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ff655-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="ff655-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ff655-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Trakopolis based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ff655-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Trakopolis based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ff655-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Trakopolis to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="ff655-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Trakopolis to an user in Azure AD is.</span></span> <span data-ttu-id="ff655-142">In other words, a link relationship between an Azure AD user and the related user in Trakopolis needs to be established.</span><span class="sxs-lookup"><span data-stu-id="ff655-142">In other words, a link relationship between an Azure AD user and the related user in Trakopolis needs to be established.</span></span>  
<span data-ttu-id="ff655-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="ff655-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Trakopolis.</span></span>

<span data-ttu-id="ff655-144">To configure and test Azure AD single sign-on with Trakopolis, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ff655-144">To configure and test Azure AD single sign-on with Trakopolis, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ff655-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="ff655-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ff655-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ff655-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ff655-147">**[Creating a Trakopolis test user](#creating-a-trakopolis-test-user)** - to have a counterpart of Britta Simon in Trakopolis that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="ff655-147">**[Creating a Trakopolis test user](#creating-a-trakopolis-test-user)** - to have a counterpart of Britta Simon in Trakopolis that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="ff655-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ff655-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ff655-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="ff655-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ff655-150">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ff655-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="ff655-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Trakopolis application.</span><span class="sxs-lookup"><span data-stu-id="ff655-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Trakopolis application.</span></span>

<span data-ttu-id="ff655-152">**To configure Azure AD single sign-on with Trakopolis, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ff655-152">**To configure Azure AD single sign-on with Trakopolis, perform the following steps:**</span></span>

1. <span data-ttu-id="ff655-153">In the Azure classic portal, on the **Trakopolis** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="ff655-153">In the Azure classic portal, on the **Trakopolis** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 

2. <span data-ttu-id="ff655-155">On the **How would you like users to sign on to Trakopolis** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ff655-155">On the **How would you like users to sign on to Trakopolis** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_03.png) 

3. <span data-ttu-id="ff655-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ff655-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_04.png) 

    <span data-ttu-id="ff655-159">a.</span><span class="sxs-lookup"><span data-stu-id="ff655-159">a.</span></span> <span data-ttu-id="ff655-160">In the Sign On URL textbox, type the URL used by your users to sign-on to your Trakopolis application using the following pattern: **“https://\<company name\>.trakopolis.com”**.</span><span class="sxs-lookup"><span data-stu-id="ff655-160">In the Sign On URL textbox, type the URL used by your users to sign-on to your Trakopolis application using the following pattern: **“https://\<company name\>.trakopolis.com”**.</span></span>

    <span data-ttu-id="ff655-161">b.</span><span class="sxs-lookup"><span data-stu-id="ff655-161">b.</span></span> <span data-ttu-id="ff655-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ff655-162">Click **Next**.</span></span>

1. <span data-ttu-id="ff655-163">On the **Configure single sign-on at Trakopolis** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ff655-163">On the **Configure single sign-on at Trakopolis** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_05.png) 
   
    <span data-ttu-id="ff655-165">a.</span><span class="sxs-lookup"><span data-stu-id="ff655-165">a.</span></span> <span data-ttu-id="ff655-166">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="ff655-166">Click **Download certificate**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="ff655-167">b.</span><span class="sxs-lookup"><span data-stu-id="ff655-167">b.</span></span> <span data-ttu-id="ff655-168">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ff655-168">Click **Next**.</span></span>

2. <span data-ttu-id="ff655-169">To get SSO configured for your application, contact your Trakopolis support team at [support@cantelematics.com](mailto:support@cantelematics.com), attach the downloaded certificate and provide them with the **Issuer URL**, the **SAML SSO URL** and the **Sign Out URL**.</span><span class="sxs-lookup"><span data-stu-id="ff655-169">To get SSO configured for your application, contact your Trakopolis support team at [support@cantelematics.com](mailto:support@cantelematics.com), attach the downloaded certificate and provide them with the **Issuer URL**, the **SAML SSO URL** and the **Sign Out URL**.</span></span>

3. <span data-ttu-id="ff655-170">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ff655-170">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]

4. <span data-ttu-id="ff655-172">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="ff655-172">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ff655-174">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ff655-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="ff655-175">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ff655-175">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="ff655-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ff655-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ff655-178">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ff655-178">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="ff655-180">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="ff655-180">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="ff655-181">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="ff655-181">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ff655-183">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="ff655-183">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="ff655-185">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ff655-185">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="ff655-187">a.</span><span class="sxs-lookup"><span data-stu-id="ff655-187">a.</span></span> <span data-ttu-id="ff655-188">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="ff655-188">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="ff655-189">b.</span><span class="sxs-lookup"><span data-stu-id="ff655-189">b.</span></span> <span data-ttu-id="ff655-190">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ff655-190">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="ff655-191">c.</span><span class="sxs-lookup"><span data-stu-id="ff655-191">c.</span></span> <span data-ttu-id="ff655-192">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ff655-192">Click **Next**.</span></span>

6. <span data-ttu-id="ff655-193">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ff655-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="ff655-195">a.</span><span class="sxs-lookup"><span data-stu-id="ff655-195">a.</span></span> <span data-ttu-id="ff655-196">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ff655-196">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="ff655-197">b.</span><span class="sxs-lookup"><span data-stu-id="ff655-197">b.</span></span> <span data-ttu-id="ff655-198">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ff655-198">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="ff655-199">c.</span><span class="sxs-lookup"><span data-stu-id="ff655-199">c.</span></span> <span data-ttu-id="ff655-200">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ff655-200">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="ff655-201">d.</span><span class="sxs-lookup"><span data-stu-id="ff655-201">d.</span></span> <span data-ttu-id="ff655-202">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="ff655-202">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="ff655-203">e.</span><span class="sxs-lookup"><span data-stu-id="ff655-203">e.</span></span> <span data-ttu-id="ff655-204">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ff655-204">Click **Next**.</span></span>

7. <span data-ttu-id="ff655-205">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="ff655-205">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="ff655-207">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ff655-207">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="ff655-209">a.</span><span class="sxs-lookup"><span data-stu-id="ff655-209">a.</span></span> <span data-ttu-id="ff655-210">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="ff655-210">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="ff655-211">b.</span><span class="sxs-lookup"><span data-stu-id="ff655-211">b.</span></span> <span data-ttu-id="ff655-212">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="ff655-212">Click **Complete**.</span></span>   

### <a name="creating-a-trakopolis-test-user"></a><span data-ttu-id="ff655-213">Creating a Trakopolis test User</span><span class="sxs-lookup"><span data-stu-id="ff655-213">Creating a Trakopolis test User</span></span>
<span data-ttu-id="ff655-214">The objective of this section is to create a user called Britta Simon in Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="ff655-214">The objective of this section is to create a user called Britta Simon in Trakopolis.</span></span>  
<span data-ttu-id="ff655-215">Please work with the Trakopolis support team to add the users in Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="ff655-215">Please work with the Trakopolis support team to add the users in Trakopolis.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ff655-216">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ff655-216">Assigning the Azure AD test user</span></span>
<span data-ttu-id="ff655-217">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Trakopolis.</span><span class="sxs-lookup"><span data-stu-id="ff655-217">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Trakopolis.</span></span>

![Assign User][200] 

<span data-ttu-id="ff655-219">**To assign Britta Simon to Trakopolis, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ff655-219">**To assign Britta Simon to Trakopolis, perform the following steps:**</span></span>

1. <span data-ttu-id="ff655-220">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="ff655-220">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 

2. <span data-ttu-id="ff655-222">In the applications list, select **Trakopolis**.</span><span class="sxs-lookup"><span data-stu-id="ff655-222">In the applications list, select **Trakopolis**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/tutorial_trakopolis_50.png) 

3. <span data-ttu-id="ff655-224">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="ff655-224">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 

4. <span data-ttu-id="ff655-226">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ff655-226">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="ff655-227">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="ff655-227">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="ff655-229">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="ff655-229">Testing Single Sign-On</span></span>
<span data-ttu-id="ff655-230">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ff655-230">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="ff655-231">When you click the Trakopolis tile in the Access Panel, you should get automatically signed-on to your Trakopolis application.</span><span class="sxs-lookup"><span data-stu-id="ff655-231">When you click the Trakopolis tile in the Access Panel, you should get automatically signed-on to your Trakopolis application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ff655-232">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="ff655-232">Additional Resources</span></span>
* [<span data-ttu-id="ff655-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff655-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ff655-234">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ff655-234">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-trakopolis-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-trakopolis-tutorial/tutorial_general_205.png

























