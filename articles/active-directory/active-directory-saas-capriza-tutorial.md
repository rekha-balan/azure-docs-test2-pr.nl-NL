---
title: 'Tutorial: Azure Active Directory integration with Capriza | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Capriza.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 48d92247-f00a-47b9-8d4e-137028d9e200
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 05009c872f09840c9aee68710c0e231fc2474441
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555099"
---
# <a name="tutorial-azure-active-directory-integration-with-capriza"></a><span data-ttu-id="59dc2-103">Tutorial: Azure Active Directory integration with Capriza</span><span class="sxs-lookup"><span data-stu-id="59dc2-103">Tutorial: Azure Active Directory integration with Capriza</span></span>
<span data-ttu-id="59dc2-104">The objective of this tutorial is to show you how to integrate Capriza with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="59dc2-104">The objective of this tutorial is to show you how to integrate Capriza with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="59dc2-105">Integrating Capriza with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="59dc2-105">Integrating Capriza with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="59dc2-106">You can control in Azure AD who has access to Capriza</span><span class="sxs-lookup"><span data-stu-id="59dc2-106">You can control in Azure AD who has access to Capriza</span></span>
* <span data-ttu-id="59dc2-107">You can enable your users to automatically get signed-on to Capriza (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="59dc2-107">You can enable your users to automatically get signed-on to Capriza (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="59dc2-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="59dc2-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="59dc2-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="59dc2-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59dc2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="59dc2-110">Prerequisites</span></span>
<span data-ttu-id="59dc2-111">To configure Azure AD integration with Capriza, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="59dc2-111">To configure Azure AD integration with Capriza, you need the following items:</span></span>

* <span data-ttu-id="59dc2-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="59dc2-112">An Azure AD subscription</span></span>
* <span data-ttu-id="59dc2-113">A Capriza single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="59dc2-113">A Capriza single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="59dc2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="59dc2-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="59dc2-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="59dc2-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="59dc2-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="59dc2-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="59dc2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="59dc2-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="59dc2-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="59dc2-118">Scenario Description</span></span>
<span data-ttu-id="59dc2-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="59dc2-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="59dc2-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="59dc2-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="59dc2-121">Adding Capriza from the gallery</span><span class="sxs-lookup"><span data-stu-id="59dc2-121">Adding Capriza from the gallery</span></span>
2. <span data-ttu-id="59dc2-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="59dc2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-capriza-from-the-gallery"></a><span data-ttu-id="59dc2-123">Adding Capriza from the gallery</span><span class="sxs-lookup"><span data-stu-id="59dc2-123">Adding Capriza from the gallery</span></span>
<span data-ttu-id="59dc2-124">To configure the integration of Capriza into Azure AD, you need to add Capriza from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="59dc2-124">To configure the integration of Capriza into Azure AD, you need to add Capriza from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="59dc2-125">**To add Capriza from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="59dc2-125">**To add Capriza from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="59dc2-126">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-126">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="59dc2-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="59dc2-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="59dc2-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="59dc2-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="59dc2-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="59dc2-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="59dc2-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="59dc2-135">In the search box, type **Capriza**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-135">In the search box, type **Capriza**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/tutorial_capriza_01.png)
7. <span data-ttu-id="59dc2-137">In the results pane, select **Capriza**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="59dc2-137">In the results pane, select **Capriza**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/tutorial_capriza_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="59dc2-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="59dc2-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="59dc2-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Capriza based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="59dc2-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Capriza based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="59dc2-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Capriza to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="59dc2-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Capriza to an user in Azure AD is.</span></span> <span data-ttu-id="59dc2-142">In other words, a link relationship between an Azure AD user and the related user in Capriza needs to be established.</span><span class="sxs-lookup"><span data-stu-id="59dc2-142">In other words, a link relationship between an Azure AD user and the related user in Capriza needs to be established.</span></span>  
<span data-ttu-id="59dc2-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Capriza.</span><span class="sxs-lookup"><span data-stu-id="59dc2-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Capriza.</span></span>

<span data-ttu-id="59dc2-144">To configure and test Azure AD single sign-on with Capriza, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="59dc2-144">To configure and test Azure AD single sign-on with Capriza, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="59dc2-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="59dc2-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="59dc2-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="59dc2-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="59dc2-147">**[Creating a Capriza test user](#creating-a-capriza-test-user)** - to have a counterpart of Britta Simon in Capriza that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="59dc2-147">**[Creating a Capriza test user](#creating-a-capriza-test-user)** - to have a counterpart of Britta Simon in Capriza that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="59dc2-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="59dc2-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="59dc2-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="59dc2-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="59dc2-150">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="59dc2-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="59dc2-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Capriza application.</span><span class="sxs-lookup"><span data-stu-id="59dc2-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Capriza application.</span></span>

<span data-ttu-id="59dc2-152">**To configure Azure AD single sign-on with Capriza, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="59dc2-152">**To configure Azure AD single sign-on with Capriza, perform the following steps:**</span></span>

1. <span data-ttu-id="59dc2-153">In the Azure classic portal, on the **Capriza** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="59dc2-153">In the Azure classic portal, on the **Capriza** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="59dc2-155">On the **How would you like users to sign on to Capriza** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-155">On the **How would you like users to sign on to Capriza** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/tutorial_capriza_03.png) 
3. <span data-ttu-id="59dc2-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="59dc2-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/tutorial_capriza_04.png) 

    <span data-ttu-id="59dc2-159">a.</span><span class="sxs-lookup"><span data-stu-id="59dc2-159">a.</span></span> <span data-ttu-id="59dc2-160">In the Sign On URL textbox, type the URL used by your users to sign-on to your Capriza application using the following pattern: **“https://companyname.capriza.com/tenantid”**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-160">In the Sign On URL textbox, type the URL used by your users to sign-on to your Capriza application using the following pattern: **“https://companyname.capriza.com/tenantid”**.</span></span>

    <span data-ttu-id="59dc2-161">b.</span><span class="sxs-lookup"><span data-stu-id="59dc2-161">b.</span></span> <span data-ttu-id="59dc2-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-162">Click **Next**.</span></span>


1. <span data-ttu-id="59dc2-163">On the **Configure single sign-on at Capriza** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="59dc2-163">On the **Configure single sign-on at Capriza** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/tutorial_capriza_05.png) 
   
    <span data-ttu-id="59dc2-165">a.</span><span class="sxs-lookup"><span data-stu-id="59dc2-165">a.</span></span> <span data-ttu-id="59dc2-166">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="59dc2-166">Click **Download certificate**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="59dc2-167">b.</span><span class="sxs-lookup"><span data-stu-id="59dc2-167">b.</span></span> <span data-ttu-id="59dc2-168">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-168">Click **Next**.</span></span>
2. <span data-ttu-id="59dc2-169">To get SSO configured for your application, contact your Capriza support team via support@capriza.com and attach the downloaded certificate file to your email.</span><span class="sxs-lookup"><span data-stu-id="59dc2-169">To get SSO configured for your application, contact your Capriza support team via support@capriza.com and attach the downloaded certificate file to your email.</span></span> <span data-ttu-id="59dc2-170">Also please do provide the SAML SSO URL, Sign Out URL and Issuer URL so that they can be configured for SSO integration.</span><span class="sxs-lookup"><span data-stu-id="59dc2-170">Also please do provide the SAML SSO URL, Sign Out URL and Issuer URL so that they can be configured for SSO integration.</span></span>
3. <span data-ttu-id="59dc2-171">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-171">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
4. <span data-ttu-id="59dc2-173">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-173">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="59dc2-175">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="59dc2-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="59dc2-176">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="59dc2-176">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Create Azure AD User][20]

<span data-ttu-id="59dc2-178">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="59dc2-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="59dc2-179">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-179">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="59dc2-181">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="59dc2-181">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="59dc2-182">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-182">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="59dc2-184">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-184">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="59dc2-186">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="59dc2-186">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="59dc2-188">a.</span><span class="sxs-lookup"><span data-stu-id="59dc2-188">a.</span></span> <span data-ttu-id="59dc2-189">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="59dc2-189">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="59dc2-190">b.</span><span class="sxs-lookup"><span data-stu-id="59dc2-190">b.</span></span> <span data-ttu-id="59dc2-191">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="59dc2-192">c.</span><span class="sxs-lookup"><span data-stu-id="59dc2-192">c.</span></span> <span data-ttu-id="59dc2-193">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-193">Click **Next**.</span></span>
6. <span data-ttu-id="59dc2-194">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="59dc2-194">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="59dc2-196">a.</span><span class="sxs-lookup"><span data-stu-id="59dc2-196">a.</span></span> <span data-ttu-id="59dc2-197">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-197">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="59dc2-198">b.</span><span class="sxs-lookup"><span data-stu-id="59dc2-198">b.</span></span> <span data-ttu-id="59dc2-199">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-199">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="59dc2-200">c.</span><span class="sxs-lookup"><span data-stu-id="59dc2-200">c.</span></span> <span data-ttu-id="59dc2-201">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-201">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="59dc2-202">d.</span><span class="sxs-lookup"><span data-stu-id="59dc2-202">d.</span></span> <span data-ttu-id="59dc2-203">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-203">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="59dc2-204">e.</span><span class="sxs-lookup"><span data-stu-id="59dc2-204">e.</span></span> <span data-ttu-id="59dc2-205">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-205">Click **Next**.</span></span>
7. <span data-ttu-id="59dc2-206">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-206">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="59dc2-208">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="59dc2-208">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="59dc2-210">a.</span><span class="sxs-lookup"><span data-stu-id="59dc2-210">a.</span></span> <span data-ttu-id="59dc2-211">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-211">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="59dc2-212">b.</span><span class="sxs-lookup"><span data-stu-id="59dc2-212">b.</span></span> <span data-ttu-id="59dc2-213">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-213">Click **Complete**.</span></span>   

### <a name="creating-a-capriza-test-user"></a><span data-ttu-id="59dc2-214">Creating a Capriza test user</span><span class="sxs-lookup"><span data-stu-id="59dc2-214">Creating a Capriza test user</span></span>
<span data-ttu-id="59dc2-215">The objective of this section is to create a user called Britta Simon in Capriza.</span><span class="sxs-lookup"><span data-stu-id="59dc2-215">The objective of this section is to create a user called Britta Simon in Capriza.</span></span> <span data-ttu-id="59dc2-216">Capriza supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="59dc2-216">Capriza supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="59dc2-217">**Please make sure that your domain name is configured with Capriza for user provisoning. After that only the just-in-time user provisioning will work.**</span><span class="sxs-lookup"><span data-stu-id="59dc2-217">**Please make sure that your domain name is configured with Capriza for user provisoning. After that only the just-in-time user provisioning will work.**</span></span>

<span data-ttu-id="59dc2-218">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="59dc2-218">There is no action item for you in this section.</span></span> <span data-ttu-id="59dc2-219">A new user will be created during an attempt to access Capriza if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="59dc2-219">A new user will be created during an attempt to access Capriza if it doesn't exist yet.</span></span> <span data-ttu-id="59dc2-220">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="59dc2-220">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

> [!NOTE]
> <span data-ttu-id="59dc2-221">If you need to create a user manually, you need to contact the Capriza support team.</span><span class="sxs-lookup"><span data-stu-id="59dc2-221">If you need to create a user manually, you need to contact the Capriza support team.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="59dc2-222">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="59dc2-222">Assigning the Azure AD test user</span></span>
<span data-ttu-id="59dc2-223">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Capriza.</span><span class="sxs-lookup"><span data-stu-id="59dc2-223">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Capriza.</span></span>

![Assign User][200] 

<span data-ttu-id="59dc2-225">**To assign Britta Simon to Capriza, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="59dc2-225">**To assign Britta Simon to Capriza, perform the following steps:**</span></span>

1. <span data-ttu-id="59dc2-226">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="59dc2-226">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="59dc2-228">In the applications list, select **Capriza**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-228">In the applications list, select **Capriza**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/tutorial_capriza_50.png) 
3. <span data-ttu-id="59dc2-230">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-230">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="59dc2-232">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-232">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="59dc2-233">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="59dc2-233">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="59dc2-235">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="59dc2-235">Testing Single Sign-On</span></span>
<span data-ttu-id="59dc2-236">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="59dc2-236">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="59dc2-237">When you click the Capriza tile in the Access Panel, you should get automatically signed-on to your Capriza application.</span><span class="sxs-lookup"><span data-stu-id="59dc2-237">When you click the Capriza tile in the Access Panel, you should get automatically signed-on to your Capriza application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="59dc2-238">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="59dc2-238">Additional Resources</span></span>
* [<span data-ttu-id="59dc2-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59dc2-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="59dc2-240">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="59dc2-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-capriza-tutorial/tutorial_general_205.png

























