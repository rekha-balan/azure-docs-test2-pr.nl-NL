---
title: 'Tutorial: Azure Active Directory integration with Small Improvements | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Small Improvements.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 59c8a112-41e1-4337-9ef3-3d7029780d61
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: jeedes
ms.openlocfilehash: 74db84c97e61d306a949a5bdece9794bb2c73092
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660538"
---
# <a name="tutorial-azure-active-directory-integration-with-small-improvements"></a><span data-ttu-id="d8acf-103">Tutorial: Azure Active Directory integration with Small Improvements</span><span class="sxs-lookup"><span data-stu-id="d8acf-103">Tutorial: Azure Active Directory integration with Small Improvements</span></span>
<span data-ttu-id="d8acf-104">The objective of this tutorial is to show you how to integrate Small Improvements with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d8acf-104">The objective of this tutorial is to show you how to integrate Small Improvements with Azure Active Directory (Azure AD).</span></span>  

<span data-ttu-id="d8acf-105">Integrating Small Improvements with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d8acf-105">Integrating Small Improvements with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="d8acf-106">You can control in Azure AD who has access to Small Improvements</span><span class="sxs-lookup"><span data-stu-id="d8acf-106">You can control in Azure AD who has access to Small Improvements</span></span>
* <span data-ttu-id="d8acf-107">You can enable your users to automatically get signed-on to Small Improvements single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="d8acf-107">You can enable your users to automatically get signed-on to Small Improvements single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="d8acf-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="d8acf-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="d8acf-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d8acf-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8acf-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d8acf-110">Prerequisites</span></span>
<span data-ttu-id="d8acf-111">To configure Azure AD integration with Small Improvements, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d8acf-111">To configure Azure AD integration with Small Improvements, you need the following items:</span></span>

* <span data-ttu-id="d8acf-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d8acf-112">An Azure AD subscription</span></span>
* <span data-ttu-id="d8acf-113">A Small Improvements SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d8acf-113">A Small Improvements SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="d8acf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d8acf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="d8acf-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d8acf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="d8acf-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="d8acf-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="d8acf-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d8acf-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d8acf-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="d8acf-118">Scenario Description</span></span>
<span data-ttu-id="d8acf-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d8acf-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>  

<span data-ttu-id="d8acf-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d8acf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d8acf-121">Adding Small Improvements from the gallery</span><span class="sxs-lookup"><span data-stu-id="d8acf-121">Adding Small Improvements from the gallery</span></span>
2. <span data-ttu-id="d8acf-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="d8acf-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-small-improvements-from-the-gallery"></a><span data-ttu-id="d8acf-123">Adding Small Improvements from the gallery</span><span class="sxs-lookup"><span data-stu-id="d8acf-123">Adding Small Improvements from the gallery</span></span>
<span data-ttu-id="d8acf-124">To configure the integration of Small Improvements into Azure AD, you need to add Small Improvements from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d8acf-124">To configure the integration of Small Improvements into Azure AD, you need to add Small Improvements from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d8acf-125">**To add Small Improvements from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d8acf-125">**To add Small Improvements from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d8acf-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="d8acf-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="d8acf-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d8acf-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="d8acf-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="d8acf-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="d8acf-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="d8acf-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="d8acf-135">In the search box, type **Small Improvements**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-135">In the search box, type **Small Improvements**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_01.png)
7. <span data-ttu-id="d8acf-137">In the results pane, select **Small Improvements**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="d8acf-137">In the results pane, select **Small Improvements**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="d8acf-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="d8acf-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="d8acf-140">The objective of this section is to show you how to configure and test Azure AD SSO with Small Improvements based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d8acf-140">The objective of this section is to show you how to configure and test Azure AD SSO with Small Improvements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d8acf-141">For SSO to work, Azure AD needs to know what the counterpart user in Small Improvements to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="d8acf-141">For SSO to work, Azure AD needs to know what the counterpart user in Small Improvements to an user in Azure AD is.</span></span> <span data-ttu-id="d8acf-142">In other words, a link relationship between an Azure AD user and the related user in Small Improvements needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d8acf-142">In other words, a link relationship between an Azure AD user and the related user in Small Improvements needs to be established.</span></span>  

<span data-ttu-id="d8acf-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Small Improvements.</span><span class="sxs-lookup"><span data-stu-id="d8acf-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Small Improvements.</span></span>

<span data-ttu-id="d8acf-144">To configure and test Azure AD SSO with Small Improvements, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d8acf-144">To configure and test Azure AD SSO with Small Improvements, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d8acf-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d8acf-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d8acf-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d8acf-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d8acf-147">**[Creating a Small Improvements test user](#creating-a-small-improvements-test-user)** - to have a counterpart of Britta Simon in Small Improvements that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="d8acf-147">**[Creating a Small Improvements test user](#creating-a-small-improvements-test-user)** - to have a counterpart of Britta Simon in Small Improvements that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="d8acf-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d8acf-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d8acf-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d8acf-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="d8acf-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="d8acf-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="d8acf-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Small Improvements application.</span><span class="sxs-lookup"><span data-stu-id="d8acf-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Small Improvements application.</span></span>

<span data-ttu-id="d8acf-152">**To configure Azure AD SSO with Small Improvements, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d8acf-152">**To configure Azure AD SSO with Small Improvements, perform the following steps:**</span></span>

1. <span data-ttu-id="d8acf-153">In the Azure classic portal, on the **Small Improvements** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="d8acf-153">In the Azure classic portal, on the **Small Improvements** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="d8acf-155">On the **How would you like users to sign on to Small Improvements** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-155">On the **How would you like users to sign on to Small Improvements** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_03.png) 
3. <span data-ttu-id="d8acf-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d8acf-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_04.png) 
   
     >[!NOTE]
     ><span data-ttu-id="d8acf-159">Contact the Small Improvements support team at [Support@small-improvements.com](mailto:support@small-improvements.com) to configure a domain name for your account.</span><span class="sxs-lookup"><span data-stu-id="d8acf-159">Contact the Small Improvements support team at [Support@small-improvements.com](mailto:support@small-improvements.com) to configure a domain name for your account.</span></span> <span data-ttu-id="d8acf-160">This is required for SSO to work.</span><span class="sxs-lookup"><span data-stu-id="d8acf-160">This is required for SSO to work.</span></span>
     >  

  1. <span data-ttu-id="d8acf-161">In the **Sign-On URL** textbox, type the URL used by your users to sign-on to your Small Improvements application.</span><span class="sxs-lookup"><span data-stu-id="d8acf-161">In the **Sign-On URL** textbox, type the URL used by your users to sign-on to your Small Improvements application.</span></span>  
  2. <span data-ttu-id="d8acf-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-162">Click **Next**.</span></span>
4. <span data-ttu-id="d8acf-163">On the **Configure single sign-on at Small Improvements** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d8acf-163">On the **Configure single sign-on at Small Improvements** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_05.png) 
 1. <span data-ttu-id="d8acf-165">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d8acf-165">Click **Download certificate**, and then save the file on your computer.</span></span>  
 2. <span data-ttu-id="d8acf-166">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-166">Click **Next**.</span></span>
2. <span data-ttu-id="d8acf-167">In another browser window, sign on to your Small Improvements company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="d8acf-167">In another browser window, sign on to your Small Improvements company site as an administrator.</span></span>
3. <span data-ttu-id="d8acf-168">From the main dashboard page, click **Administration** button on the left.</span><span class="sxs-lookup"><span data-stu-id="d8acf-168">From the main dashboard page, click **Administration** button on the left.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_06.png) 
4. <span data-ttu-id="d8acf-170">Click the **SAML SSO** button from **Integrations** section.</span><span class="sxs-lookup"><span data-stu-id="d8acf-170">Click the **SAML SSO** button from **Integrations** section.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_07.png) 
5. <span data-ttu-id="d8acf-172">On the SSO Setup page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d8acf-172">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_08.png)  
 1. <span data-ttu-id="d8acf-174">In the Azure classic portal, on the **Configure single sign-on at Small Improvements** dialog page, copy the **SAML SSO URL** value, and then paste it into the **HTTP Endpoint** textbox.</span><span class="sxs-lookup"><span data-stu-id="d8acf-174">In the Azure classic portal, on the **Configure single sign-on at Small Improvements** dialog page, copy the **SAML SSO URL** value, and then paste it into the **HTTP Endpoint** textbox.</span></span>  
 2. <span data-ttu-id="d8acf-175">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **x509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="d8acf-175">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **x509 Certificate** textbox.</span></span> 
 3. <span data-ttu-id="d8acf-176">If you wish to have SSO and Login form authentication option available for users then check the **Enable access via login/password too** option.</span><span class="sxs-lookup"><span data-stu-id="d8acf-176">If you wish to have SSO and Login form authentication option available for users then check the **Enable access via login/password too** option.</span></span>  
 4. <span data-ttu-id="d8acf-177">Enter the appropriate value to Name the SSO Login button in the **SAML Prompt** textbox.</span><span class="sxs-lookup"><span data-stu-id="d8acf-177">Enter the appropriate value to Name the SSO Login button in the **SAML Prompt** textbox.</span></span>  
 5. <span data-ttu-id="d8acf-178">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-178">Click **Save**.</span></span>
6. <span data-ttu-id="d8acf-179">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-179">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="d8acf-181">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-181">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d8acf-183">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d8acf-183">Create an Azure AD test user</span></span>
<span data-ttu-id="d8acf-184">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d8acf-184">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Create Azure AD User][20]

<span data-ttu-id="d8acf-186">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d8acf-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d8acf-187">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-187">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="d8acf-189">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="d8acf-189">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d8acf-190">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-190">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="d8acf-192">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-192">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="d8acf-194">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d8acf-194">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/create_aaduser_05.png) 
 1. <span data-ttu-id="d8acf-196">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="d8acf-196">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="d8acf-197">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-197">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="d8acf-198">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-198">Click **Next**.</span></span>
6. <span data-ttu-id="d8acf-199">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d8acf-199">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="d8acf-201">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-201">In the **First Name** textbox, type **Britta**.</span></span>   
 2. <span data-ttu-id="d8acf-202">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-202">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="d8acf-203">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-203">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="d8acf-204">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-204">In the **Role** list, select **User**.</span></span> 
 5. <span data-ttu-id="d8acf-205">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-205">Click **Next**.</span></span>
7. <span data-ttu-id="d8acf-206">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-206">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="d8acf-208">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d8acf-208">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/create_aaduser_08.png) 
 1. <span data-ttu-id="d8acf-210">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-210">Write down the value of the **New Password**.</span></span> 
 2. <span data-ttu-id="d8acf-211">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-211">Click **Complete**.</span></span>   

### <a name="create-a-small-improvements-test-user"></a><span data-ttu-id="d8acf-212">Create a Small Improvements test user</span><span class="sxs-lookup"><span data-stu-id="d8acf-212">Create a Small Improvements test user</span></span>
<span data-ttu-id="d8acf-213">The objective of this section is to create a user called Britta Simon in Small Improvements.</span><span class="sxs-lookup"><span data-stu-id="d8acf-213">The objective of this section is to create a user called Britta Simon in Small Improvements.</span></span>

<span data-ttu-id="d8acf-214">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="d8acf-214">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

<span data-ttu-id="d8acf-215">**To create a user called Britta Simon in Small Improvements, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d8acf-215">**To create a user called Britta Simon in Small Improvements, perform the following steps:**</span></span>

1. <span data-ttu-id="d8acf-216">Sign-on to your Small Improvements company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="d8acf-216">Sign-on to your Small Improvements company site as an administrator.</span></span>
2. <span data-ttu-id="d8acf-217">From the Home page, go to the menu on the left, click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-217">From the Home page, go to the menu on the left, click **Administration**.</span></span>
3. <span data-ttu-id="d8acf-218">Click the **User Directory** button from User Management section.</span><span class="sxs-lookup"><span data-stu-id="d8acf-218">Click the **User Directory** button from User Management section.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_10.png) 
4. <span data-ttu-id="d8acf-220">Click **Add Team Member**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-220">Click **Add Team Member**.</span></span>
    <span data-ttu-id="d8acf-221">![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_11.png)</span><span class="sxs-lookup"><span data-stu-id="d8acf-221">![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_11.png)</span></span> 
5. <span data-ttu-id="d8acf-222">Type the **First Name**, **Last Name** and **Email Address** of a valid user you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="d8acf-222">Type the **First Name**, **Last Name** and **Email Address** of a valid user you want to provision into the related textboxes.</span></span> 
    <span data-ttu-id="d8acf-223">![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_12.png)</span><span class="sxs-lookup"><span data-stu-id="d8acf-223">![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_12.png)</span></span> 
6. <span data-ttu-id="d8acf-224">You can also choose to enter the personal message in the **Send notification email** box.</span><span class="sxs-lookup"><span data-stu-id="d8acf-224">You can also choose to enter the personal message in the **Send notification email** box.</span></span> <span data-ttu-id="d8acf-225">If you do not wish to send the notification then uncheck this checkbox.</span><span class="sxs-lookup"><span data-stu-id="d8acf-225">If you do not wish to send the notification then uncheck this checkbox.</span></span>
7. <span data-ttu-id="d8acf-226">Click **Create Users**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-226">Click **Create Users**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d8acf-227">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d8acf-227">Assign the Azure AD test user</span></span>
<span data-ttu-id="d8acf-228">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Small Improvements.</span><span class="sxs-lookup"><span data-stu-id="d8acf-228">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Small Improvements.</span></span>

    ![Assign User][200] 

<span data-ttu-id="d8acf-229">**To assign Britta Simon to Small Improvements, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d8acf-229">**To assign Britta Simon to Small Improvements, perform the following steps:**</span></span>

1. <span data-ttu-id="d8acf-230">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="d8acf-230">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="d8acf-232">In the applications list, select **Small Improvements**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-232">In the applications list, select **Small Improvements**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_smallimprovements_50.png) 
3. <span data-ttu-id="d8acf-234">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-234">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="d8acf-236">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-236">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="d8acf-237">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="d8acf-237">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="d8acf-239">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="d8acf-239">Test single sign-on</span></span>
<span data-ttu-id="d8acf-240">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d8acf-240">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="d8acf-241">When you click the Small Improvements tile in the Access Panel, you should get automatically signed-on to your Small Improvements application.</span><span class="sxs-lookup"><span data-stu-id="d8acf-241">When you click the Small Improvements tile in the Access Panel, you should get automatically signed-on to your Small Improvements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d8acf-242">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="d8acf-242">Additional Resources</span></span>
* [<span data-ttu-id="d8acf-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8acf-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d8acf-244">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d8acf-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-smallimprovements-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-smallimprovements-tutorial/tutorial_general_205.png































