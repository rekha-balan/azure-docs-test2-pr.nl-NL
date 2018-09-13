---
title: 'Tutorial: Azure Active Directory integration with Insperity ExpensAble | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Insperity ExpensAble.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: c579c453-580e-417d-8a5e-9b6b352795c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 6df2c5c317125756011240fbba6ba362566b1ba3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564503"
---
# <a name="tutorial-azure-active-directory-integration-with-insperity-expensable"></a><span data-ttu-id="63966-103">Tutorial: Azure Active Directory integration with Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="63966-103">Tutorial: Azure Active Directory integration with Insperity ExpensAble</span></span>
<span data-ttu-id="63966-104">The objective of this tutorial is to show you how to integrate Insperity ExpensAble with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="63966-104">The objective of this tutorial is to show you how to integrate Insperity ExpensAble with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="63966-105">Integrating Insperity ExpensAble with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="63966-105">Integrating Insperity ExpensAble with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="63966-106">You can control in Azure AD who has access to Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="63966-106">You can control in Azure AD who has access to Insperity ExpensAble</span></span>
* <span data-ttu-id="63966-107">You can enable your users to automatically get signed-on to Insperity ExpensAble (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="63966-107">You can enable your users to automatically get signed-on to Insperity ExpensAble (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="63966-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="63966-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="63966-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="63966-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63966-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="63966-110">Prerequisites</span></span>
<span data-ttu-id="63966-111">To configure Azure AD integration with Insperity ExpensAble, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="63966-111">To configure Azure AD integration with Insperity ExpensAble, you need the following items:</span></span>

* <span data-ttu-id="63966-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="63966-112">An Azure AD subscription</span></span>
* <span data-ttu-id="63966-113">A Insperity ExpensAble single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="63966-113">A Insperity ExpensAble single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="63966-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="63966-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="63966-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="63966-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="63966-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="63966-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="63966-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="63966-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="63966-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="63966-118">Scenario Description</span></span>
<span data-ttu-id="63966-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="63966-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="63966-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="63966-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="63966-121">Adding Insperity ExpensAble from the gallery</span><span class="sxs-lookup"><span data-stu-id="63966-121">Adding Insperity ExpensAble from the gallery</span></span>
2. <span data-ttu-id="63966-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="63966-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insperity-expensable-from-the-gallery"></a><span data-ttu-id="63966-123">Adding Insperity ExpensAble from the gallery</span><span class="sxs-lookup"><span data-stu-id="63966-123">Adding Insperity ExpensAble from the gallery</span></span>
<span data-ttu-id="63966-124">To configure the integration of Insperity ExpensAble into Azure AD, you need to add Insperity ExpensAble from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="63966-124">To configure the integration of Insperity ExpensAble into Azure AD, you need to add Insperity ExpensAble from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="63966-125">**To add Insperity ExpensAble from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="63966-125">**To add Insperity ExpensAble from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="63966-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="63966-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="63966-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="63966-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="63966-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="63966-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="63966-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="63966-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="63966-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="63966-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="63966-135">In the search box, type **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="63966-135">In the search box, type **Insperity ExpensAble**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_01.png)
7. <span data-ttu-id="63966-137">In the results pane, select **Insperity ExpensAble**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="63966-137">In the results pane, select **Insperity ExpensAble**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="63966-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="63966-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="63966-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Insperity ExpensAble based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="63966-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Insperity ExpensAble based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="63966-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Insperity ExpensAble to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="63966-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Insperity ExpensAble to an user in Azure AD is.</span></span> <span data-ttu-id="63966-142">In other words, a link relationship between an Azure AD user and the related user in Insperity ExpensAble needs to be established.</span><span class="sxs-lookup"><span data-stu-id="63966-142">In other words, a link relationship between an Azure AD user and the related user in Insperity ExpensAble needs to be established.</span></span>  
<span data-ttu-id="63966-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="63966-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Insperity ExpensAble.</span></span>

<span data-ttu-id="63966-144">To configure and test Azure AD single sign-on with Insperity ExpensAble, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="63966-144">To configure and test Azure AD single sign-on with Insperity ExpensAble, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="63966-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="63966-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="63966-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="63966-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="63966-147">**[Creating a Insperity ExpensAble test user](#creating-a-insperityexpensable-test-user)** - to have a counterpart of Britta Simon in Insperity ExpensAble that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="63966-147">**[Creating a Insperity ExpensAble test user](#creating-a-insperityexpensable-test-user)** - to have a counterpart of Britta Simon in Insperity ExpensAble that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="63966-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="63966-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="63966-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="63966-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="63966-150">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="63966-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="63966-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Insperity ExpensAble application.</span><span class="sxs-lookup"><span data-stu-id="63966-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Insperity ExpensAble application.</span></span>

<span data-ttu-id="63966-152">**To configure Azure AD single sign-on with Insperity ExpensAble, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="63966-152">**To configure Azure AD single sign-on with Insperity ExpensAble, perform the following steps:**</span></span>

1. <span data-ttu-id="63966-153">In the Azure classic portal, on the **Insperity ExpensAble** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="63966-153">In the Azure classic portal, on the **Insperity ExpensAble** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="63966-155">On the **How would you like users to sign on to Insperity ExpensAble** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="63966-155">On the **How would you like users to sign on to Insperity ExpensAble** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_03.png) 
3. <span data-ttu-id="63966-157">On the **Configure App Settings** dialog page, perform the following steps:.</span><span class="sxs-lookup"><span data-stu-id="63966-157">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_04.png) 

    <span data-ttu-id="63966-159">a.</span><span class="sxs-lookup"><span data-stu-id="63966-159">a.</span></span> <span data-ttu-id="63966-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Insperity ExpensAble application using the following pattern: `https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span><span class="sxs-lookup"><span data-stu-id="63966-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Insperity ExpensAble application using the following pattern: `https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span></span>

    <span data-ttu-id="63966-161">b.</span><span class="sxs-lookup"><span data-stu-id="63966-161">b.</span></span> <span data-ttu-id="63966-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="63966-162">Click **Next**.</span></span>

1. <span data-ttu-id="63966-163">On the **Configure single sign-on at Insperity ExpensAble** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="63966-163">On the **Configure single sign-on at Insperity ExpensAble** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_05.png) 
   
    <span data-ttu-id="63966-165">a.</span><span class="sxs-lookup"><span data-stu-id="63966-165">a.</span></span> <span data-ttu-id="63966-166">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="63966-166">Click **Download certificate**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="63966-167">b.</span><span class="sxs-lookup"><span data-stu-id="63966-167">b.</span></span> <span data-ttu-id="63966-168">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="63966-168">Click **Next**.</span></span>

2. <span data-ttu-id="63966-169">To get SSO configured for your application, contact your Insperity ExpensAble technical support team.</span><span class="sxs-lookup"><span data-stu-id="63966-169">To get SSO configured for your application, contact your Insperity ExpensAble technical support team.</span></span> <span data-ttu-id="63966-170">Once the case is assigned then email the downloaded certificate file.</span><span class="sxs-lookup"><span data-stu-id="63966-170">Once the case is assigned then email the downloaded certificate file.</span></span> <span data-ttu-id="63966-171">Also please do provide the Issuer URL and Single Sign On Service URL so that they can be configured for SSO integration.</span><span class="sxs-lookup"><span data-stu-id="63966-171">Also please do provide the Issuer URL and Single Sign On Service URL so that they can be configured for SSO integration.</span></span> 

3. <span data-ttu-id="63966-172">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="63966-172">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
4. <span data-ttu-id="63966-174">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="63966-174">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="63966-176">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="63966-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="63966-177">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="63966-177">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Create Azure AD User][20]

<span data-ttu-id="63966-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="63966-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="63966-180">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="63966-180">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="63966-182">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="63966-182">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="63966-183">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="63966-183">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="63966-185">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="63966-185">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="63966-187">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="63966-187">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="63966-189">a.</span><span class="sxs-lookup"><span data-stu-id="63966-189">a.</span></span> <span data-ttu-id="63966-190">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="63966-190">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="63966-191">b.</span><span class="sxs-lookup"><span data-stu-id="63966-191">b.</span></span> <span data-ttu-id="63966-192">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="63966-192">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="63966-193">c.</span><span class="sxs-lookup"><span data-stu-id="63966-193">c.</span></span> <span data-ttu-id="63966-194">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="63966-194">Click **Next**.</span></span>
6. <span data-ttu-id="63966-195">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="63966-195">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="63966-197">a.</span><span class="sxs-lookup"><span data-stu-id="63966-197">a.</span></span> <span data-ttu-id="63966-198">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="63966-198">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="63966-199">b.</span><span class="sxs-lookup"><span data-stu-id="63966-199">b.</span></span> <span data-ttu-id="63966-200">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="63966-200">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="63966-201">c.</span><span class="sxs-lookup"><span data-stu-id="63966-201">c.</span></span> <span data-ttu-id="63966-202">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="63966-202">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="63966-203">d.</span><span class="sxs-lookup"><span data-stu-id="63966-203">d.</span></span> <span data-ttu-id="63966-204">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="63966-204">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="63966-205">e.</span><span class="sxs-lookup"><span data-stu-id="63966-205">e.</span></span> <span data-ttu-id="63966-206">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="63966-206">Click **Next**.</span></span>

7. <span data-ttu-id="63966-207">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="63966-207">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="63966-209">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="63966-209">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="63966-211">a.</span><span class="sxs-lookup"><span data-stu-id="63966-211">a.</span></span> <span data-ttu-id="63966-212">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="63966-212">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="63966-213">b.</span><span class="sxs-lookup"><span data-stu-id="63966-213">b.</span></span> <span data-ttu-id="63966-214">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="63966-214">Click **Complete**.</span></span>   

### <a name="creating-a-insperity-expensable-test-user"></a><span data-ttu-id="63966-215">Creating a Insperity ExpensAble test user</span><span class="sxs-lookup"><span data-stu-id="63966-215">Creating a Insperity ExpensAble test user</span></span>
<span data-ttu-id="63966-216">The objective of this section is to create a user called Britta Simon in Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="63966-216">The objective of this section is to create a user called Britta Simon in Insperity ExpensAble.</span></span> <span data-ttu-id="63966-217">Please work with Insperity ExpensAble support team to add the users in the Insperity ExpensAble account.</span><span class="sxs-lookup"><span data-stu-id="63966-217">Please work with Insperity ExpensAble support team to add the users in the Insperity ExpensAble account.</span></span> 

> [!NOTE]
> <span data-ttu-id="63966-218">If you need to create an user manually, you need to contact the Insperity ExpensAble support team.</span><span class="sxs-lookup"><span data-stu-id="63966-218">If you need to create an user manually, you need to contact the Insperity ExpensAble support team.</span></span>
> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="63966-219">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="63966-219">Assigning the Azure AD test user</span></span>
<span data-ttu-id="63966-220">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="63966-220">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Insperity ExpensAble.</span></span>

![Assign User][200] 

<span data-ttu-id="63966-222">**To assign Britta Simon to Insperity ExpensAble, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="63966-222">**To assign Britta Simon to Insperity ExpensAble, perform the following steps:**</span></span>

1. <span data-ttu-id="63966-223">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="63966-223">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="63966-225">In the applications list, select **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="63966-225">In the applications list, select **Insperity ExpensAble**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_50.png) 
3. <span data-ttu-id="63966-227">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="63966-227">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="63966-229">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="63966-229">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="63966-230">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="63966-230">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="63966-232">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="63966-232">Testing Single Sign-On</span></span>
<span data-ttu-id="63966-233">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="63966-233">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="63966-234">When you click the Insperity ExpensAble tile in the Access Panel, you should get automatically signed-on to your Insperity ExpensAble application.</span><span class="sxs-lookup"><span data-stu-id="63966-234">When you click the Insperity ExpensAble tile in the Access Panel, you should get automatically signed-on to your Insperity ExpensAble application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="63966-235">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="63966-235">Additional Resources</span></span>
* [<span data-ttu-id="63966-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="63966-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="63966-237">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="63966-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_205.png

























