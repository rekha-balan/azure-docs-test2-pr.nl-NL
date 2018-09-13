---
title: 'Tutorial: Azure Active Directory integration with HPE SaaS | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and HPE SaaS.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 314003d6-ca66-4456-88c3-934254d4a9a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 52decf7a31eb1313da66602b2c254c2fb8ee5853
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563136"
---
# <a name="tutorial-azure-active-directory-integration-with-hpe-saas"></a><span data-ttu-id="3075c-103">Tutorial: Azure Active Directory integration with HPE SaaS</span><span class="sxs-lookup"><span data-stu-id="3075c-103">Tutorial: Azure Active Directory integration with HPE SaaS</span></span>
<span data-ttu-id="3075c-104">The objective of this tutorial is to show you how to integrate HPE SaaS with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3075c-104">The objective of this tutorial is to show you how to integrate HPE SaaS with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="3075c-105">Integrating HPE SaaS with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="3075c-105">Integrating HPE SaaS with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="3075c-106">You can control in Azure AD who has access to HPE SaaS</span><span class="sxs-lookup"><span data-stu-id="3075c-106">You can control in Azure AD who has access to HPE SaaS</span></span>
* <span data-ttu-id="3075c-107">You can enable your users to automatically get signed-on to HPE SaaS (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="3075c-107">You can enable your users to automatically get signed-on to HPE SaaS (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="3075c-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="3075c-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="3075c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3075c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3075c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3075c-110">Prerequisites</span></span>
<span data-ttu-id="3075c-111">To configure Azure AD integration with HPE SaaS, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="3075c-111">To configure Azure AD integration with HPE SaaS, you need the following items:</span></span>

* <span data-ttu-id="3075c-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="3075c-112">An Azure AD subscription</span></span>
* <span data-ttu-id="3075c-113">A HPE SaaS single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="3075c-113">A HPE SaaS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3075c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="3075c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="3075c-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="3075c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="3075c-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="3075c-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="3075c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3075c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3075c-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="3075c-118">Scenario Description</span></span>
<span data-ttu-id="3075c-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="3075c-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="3075c-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="3075c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3075c-121">Adding HPE SaaS from the gallery</span><span class="sxs-lookup"><span data-stu-id="3075c-121">Adding HPE SaaS from the gallery</span></span>
2. <span data-ttu-id="3075c-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3075c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hpe-saas-from-the-gallery"></a><span data-ttu-id="3075c-123">Adding HPE SaaS from the gallery</span><span class="sxs-lookup"><span data-stu-id="3075c-123">Adding HPE SaaS from the gallery</span></span>
<span data-ttu-id="3075c-124">To configure the integration of HPE SaaS into Azure AD, you need to add HPE SaaS from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="3075c-124">To configure the integration of HPE SaaS into Azure AD, you need to add HPE SaaS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3075c-125">**To add HPE SaaS from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3075c-125">**To add HPE SaaS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3075c-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3075c-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="3075c-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="3075c-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="3075c-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="3075c-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="3075c-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="3075c-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="3075c-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="3075c-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="3075c-135">In the search box, type **HPE SaaS**.</span><span class="sxs-lookup"><span data-stu-id="3075c-135">In the search box, type **HPE SaaS**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_01.png)
7. <span data-ttu-id="3075c-137">In the results pane, select **HPE SaaS**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="3075c-137">In the results pane, select **HPE SaaS**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3075c-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="3075c-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3075c-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with HPE SaaS based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="3075c-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with HPE SaaS based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3075c-141">For single sign-on to work, Azure AD needs to know what the counterpart user in HPE SaaS to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="3075c-141">For single sign-on to work, Azure AD needs to know what the counterpart user in HPE SaaS to an user in Azure AD is.</span></span> <span data-ttu-id="3075c-142">In other words, a link relationship between an Azure AD user and the related user in HPE SaaS needs to be established.</span><span class="sxs-lookup"><span data-stu-id="3075c-142">In other words, a link relationship between an Azure AD user and the related user in HPE SaaS needs to be established.</span></span>  
<span data-ttu-id="3075c-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="3075c-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in HPE SaaS.</span></span>

<span data-ttu-id="3075c-144">To configure and test Azure AD single sign-on with HPE SaaS, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="3075c-144">To configure and test Azure AD single sign-on with HPE SaaS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3075c-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="3075c-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3075c-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3075c-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3075c-147">**[Creating a HPE SaaS test user](#creating-a-hpesaas-test-user)** - to have a counterpart of Britta Simon in HPE SaaS that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="3075c-147">**[Creating a HPE SaaS test user](#creating-a-hpesaas-test-user)** - to have a counterpart of Britta Simon in HPE SaaS that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="3075c-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="3075c-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3075c-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="3075c-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3075c-150">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3075c-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="3075c-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your HPE SaaS application.</span><span class="sxs-lookup"><span data-stu-id="3075c-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your HPE SaaS application.</span></span>

<span data-ttu-id="3075c-152">**To configure Azure AD single sign-on with HPE SaaS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3075c-152">**To configure Azure AD single sign-on with HPE SaaS, perform the following steps:**</span></span>

1. <span data-ttu-id="3075c-153">In the Azure classic portal, on the **HPE SaaS** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="3075c-153">In the Azure classic portal, on the **HPE SaaS** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="3075c-155">On the **How would you like users to sign on to HPE SaaS** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3075c-155">On the **How would you like users to sign on to HPE SaaS** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_03.png) 
3. <span data-ttu-id="3075c-157">On the **Configure App Settings** dialog page, perform the following steps:.</span><span class="sxs-lookup"><span data-stu-id="3075c-157">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_04.png) 

    <span data-ttu-id="3075c-159">a.</span><span class="sxs-lookup"><span data-stu-id="3075c-159">a.</span></span> <span data-ttu-id="3075c-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your HPE SaaS application: **“https://login.saas.hpe.com/msg”**.</span><span class="sxs-lookup"><span data-stu-id="3075c-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your HPE SaaS application: **“https://login.saas.hpe.com/msg”**.</span></span> <span data-ttu-id="3075c-161">Customers can also change this to application specific URL.</span><span class="sxs-lookup"><span data-stu-id="3075c-161">Customers can also change this to application specific URL.</span></span>

    <span data-ttu-id="3075c-162">b.</span><span class="sxs-lookup"><span data-stu-id="3075c-162">b.</span></span> <span data-ttu-id="3075c-163">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3075c-163">Click **Next**.</span></span>


1. <span data-ttu-id="3075c-164">On the **Configure single sign-on at HPE SaaS** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3075c-164">On the **Configure single sign-on at HPE SaaS** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_05.png) 
   
    <span data-ttu-id="3075c-166">a.</span><span class="sxs-lookup"><span data-stu-id="3075c-166">a.</span></span> <span data-ttu-id="3075c-167">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="3075c-167">Click **Download metadata**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="3075c-168">b.</span><span class="sxs-lookup"><span data-stu-id="3075c-168">b.</span></span> <span data-ttu-id="3075c-169">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3075c-169">Click **Next**.</span></span>
2. <span data-ttu-id="3075c-170">To get SSO configured for your application, contact your HPE SaaS support team and email the attach downloaded metadata file.</span><span class="sxs-lookup"><span data-stu-id="3075c-170">To get SSO configured for your application, contact your HPE SaaS support team and email the attach downloaded metadata file.</span></span> <span data-ttu-id="3075c-171">So that they can be configured for SSO integration.</span><span class="sxs-lookup"><span data-stu-id="3075c-171">So that they can be configured for SSO integration.</span></span>
3. <span data-ttu-id="3075c-172">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3075c-172">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
4. <span data-ttu-id="3075c-174">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="3075c-174">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3075c-176">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3075c-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="3075c-177">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3075c-177">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Create Azure AD User][20]

<span data-ttu-id="3075c-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3075c-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3075c-180">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3075c-180">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/create_aaduser_09.png) 

1. <span data-ttu-id="3075c-182">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="3075c-182">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
2. <span data-ttu-id="3075c-183">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="3075c-183">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/create_aaduser_03.png) 
3. <span data-ttu-id="3075c-185">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="3075c-185">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/create_aaduser_04.png) 
4. <span data-ttu-id="3075c-187">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3075c-187">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="3075c-189">a.</span><span class="sxs-lookup"><span data-stu-id="3075c-189">a.</span></span> <span data-ttu-id="3075c-190">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="3075c-190">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="3075c-191">b.</span><span class="sxs-lookup"><span data-stu-id="3075c-191">b.</span></span> <span data-ttu-id="3075c-192">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3075c-192">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="3075c-193">c.</span><span class="sxs-lookup"><span data-stu-id="3075c-193">c.</span></span> <span data-ttu-id="3075c-194">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3075c-194">Click **Next**.</span></span>
5. <span data-ttu-id="3075c-195">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3075c-195">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="3075c-197">a.</span><span class="sxs-lookup"><span data-stu-id="3075c-197">a.</span></span> <span data-ttu-id="3075c-198">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="3075c-198">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="3075c-199">b.</span><span class="sxs-lookup"><span data-stu-id="3075c-199">b.</span></span> <span data-ttu-id="3075c-200">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="3075c-200">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="3075c-201">c.</span><span class="sxs-lookup"><span data-stu-id="3075c-201">c.</span></span> <span data-ttu-id="3075c-202">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3075c-202">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="3075c-203">d.</span><span class="sxs-lookup"><span data-stu-id="3075c-203">d.</span></span> <span data-ttu-id="3075c-204">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="3075c-204">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="3075c-205">e.</span><span class="sxs-lookup"><span data-stu-id="3075c-205">e.</span></span> <span data-ttu-id="3075c-206">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="3075c-206">Click **Next**.</span></span>
6. <span data-ttu-id="3075c-207">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="3075c-207">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/create_aaduser_07.png) 
7. <span data-ttu-id="3075c-209">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="3075c-209">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="3075c-211">a.</span><span class="sxs-lookup"><span data-stu-id="3075c-211">a.</span></span> <span data-ttu-id="3075c-212">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="3075c-212">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="3075c-213">b.</span><span class="sxs-lookup"><span data-stu-id="3075c-213">b.</span></span> <span data-ttu-id="3075c-214">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="3075c-214">Click **Complete**.</span></span>   

### <a name="creating-a-hpe-saas-test-user"></a><span data-ttu-id="3075c-215">Creating a HPE SaaS test user</span><span class="sxs-lookup"><span data-stu-id="3075c-215">Creating a HPE SaaS test user</span></span>
<span data-ttu-id="3075c-216">The objective of this section is to create a user called Britta Simon in HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="3075c-216">The objective of this section is to create a user called Britta Simon in HPE SaaS.</span></span> <span data-ttu-id="3075c-217">Please work with HPE SaaS support team to add the users in the HPE SaaS account.</span><span class="sxs-lookup"><span data-stu-id="3075c-217">Please work with HPE SaaS support team to add the users in the HPE SaaS account.</span></span> 

> [!NOTE]
> <span data-ttu-id="3075c-218">If you need to create an user manually, you need to contact the HPE SaaS support team.</span><span class="sxs-lookup"><span data-stu-id="3075c-218">If you need to create an user manually, you need to contact the HPE SaaS support team.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3075c-219">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="3075c-219">Assigning the Azure AD test user</span></span>
<span data-ttu-id="3075c-220">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to HPE SaaS.</span><span class="sxs-lookup"><span data-stu-id="3075c-220">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to HPE SaaS.</span></span>

![Assign User][200] 

<span data-ttu-id="3075c-222">**To assign Britta Simon to HPE SaaS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="3075c-222">**To assign Britta Simon to HPE SaaS, perform the following steps:**</span></span>

1. <span data-ttu-id="3075c-223">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="3075c-223">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="3075c-225">In the applications list, select **HPE SaaS**.</span><span class="sxs-lookup"><span data-stu-id="3075c-225">In the applications list, select **HPE SaaS**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/tutorial_hpesaas_50.png) 
3. <span data-ttu-id="3075c-227">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="3075c-227">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="3075c-229">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3075c-229">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="3075c-230">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="3075c-230">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="3075c-232">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="3075c-232">Testing Single Sign-On</span></span>
<span data-ttu-id="3075c-233">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="3075c-233">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="3075c-234">When you click the HPE SaaS tile in the Access Panel, you should get automatically signed-on to your HPE SaaS application.</span><span class="sxs-lookup"><span data-stu-id="3075c-234">When you click the HPE SaaS tile in the Access Panel, you should get automatically signed-on to your HPE SaaS application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3075c-235">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="3075c-235">Additional Resources</span></span>
* [<span data-ttu-id="3075c-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3075c-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3075c-237">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3075c-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-hpesaas-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hpesaas-tutorial/tutorial_general_205.png

























