---
title: 'Tutorial: Azure Active Directory integration with Ariba | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Ariba.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 45a8364c-55d1-4dc7-b079-9eb2a701842d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 8d8fc7199b8df427e03b9f1228152a383476d8d2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661174"
---
# <a name="tutorial-azure-active-directory-integration-with-ariba"></a><span data-ttu-id="9ff42-103">Tutorial: Azure Active Directory integration with Ariba</span><span class="sxs-lookup"><span data-stu-id="9ff42-103">Tutorial: Azure Active Directory integration with Ariba</span></span>
<span data-ttu-id="9ff42-104">The objective of this tutorial is to show you how to integrate Ariba with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9ff42-104">The objective of this tutorial is to show you how to integrate Ariba with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9ff42-105">Integrating Ariba with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="9ff42-105">Integrating Ariba with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="9ff42-106">You can control in Azure AD who has access to Ariba</span><span class="sxs-lookup"><span data-stu-id="9ff42-106">You can control in Azure AD who has access to Ariba</span></span>
* <span data-ttu-id="9ff42-107">You can enable your users to automatically get signed-on to Ariba single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="9ff42-107">You can enable your users to automatically get signed-on to Ariba single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="9ff42-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="9ff42-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="9ff42-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9ff42-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ff42-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9ff42-110">Prerequisites</span></span>
<span data-ttu-id="9ff42-111">To configure Azure AD integration with Ariba, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="9ff42-111">To configure Azure AD integration with Ariba, you need the following items:</span></span>

* <span data-ttu-id="9ff42-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="9ff42-112">An Azure AD subscription</span></span>
* <span data-ttu-id="9ff42-113">A Ariba single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="9ff42-113">A Ariba single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="9ff42-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="9ff42-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>  

<span data-ttu-id="9ff42-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="9ff42-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="9ff42-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="9ff42-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="9ff42-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9ff42-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9ff42-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="9ff42-118">Scenario Description</span></span>
<span data-ttu-id="9ff42-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="9ff42-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="9ff42-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="9ff42-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9ff42-121">Adding Ariba from the gallery</span><span class="sxs-lookup"><span data-stu-id="9ff42-121">Adding Ariba from the gallery</span></span>
2. <span data-ttu-id="9ff42-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="9ff42-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-ariba-from-the-gallery"></a><span data-ttu-id="9ff42-123">Add Ariba from the gallery</span><span class="sxs-lookup"><span data-stu-id="9ff42-123">Add Ariba from the gallery</span></span>
<span data-ttu-id="9ff42-124">To configure the integration of Ariba into Azure AD, you need to add Ariba from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="9ff42-124">To configure the integration of Ariba into Azure AD, you need to add Ariba from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9ff42-125">**To add Ariba from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9ff42-125">**To add Ariba from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9ff42-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="9ff42-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="9ff42-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="9ff42-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="9ff42-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="9ff42-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="9ff42-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="9ff42-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="9ff42-135">In the search box, type **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-135">In the search box, type **Ariba**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/tutorial_ariba_01.png)
7. <span data-ttu-id="9ff42-137">In the results pane, select **Ariba**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="9ff42-137">In the results pane, select **Ariba**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/tutorial_ariba_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="9ff42-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="9ff42-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="9ff42-140">The objective of this section is to show you how to configure and test Azure AD SSO with Ariba based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9ff42-140">The objective of this section is to show you how to configure and test Azure AD SSO with Ariba based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9ff42-141">For SSO to work, Azure AD needs to know what the counterpart user in Ariba to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="9ff42-141">For SSO to work, Azure AD needs to know what the counterpart user in Ariba to an user in Azure AD is.</span></span> <span data-ttu-id="9ff42-142">In other words, a link relationship between an Azure AD user and the related user in Ariba needs to be established.</span><span class="sxs-lookup"><span data-stu-id="9ff42-142">In other words, a link relationship between an Azure AD user and the related user in Ariba needs to be established.</span></span>

<span data-ttu-id="9ff42-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Ariba.</span><span class="sxs-lookup"><span data-stu-id="9ff42-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Ariba.</span></span>

<span data-ttu-id="9ff42-144">To configure and test Azure AD SSO with Ariba, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="9ff42-144">To configure and test Azure AD SSO with Ariba, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9ff42-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="9ff42-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9ff42-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9ff42-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9ff42-147">**[Creating a Ariba test user](#creating-a-ariba-test-user)** - to have a counterpart of Britta Simon in Ariba that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="9ff42-147">**[Creating a Ariba test user](#creating-a-ariba-test-user)** - to have a counterpart of Britta Simon in Ariba that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="9ff42-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9ff42-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9ff42-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="9ff42-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="9ff42-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="9ff42-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="9ff42-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Ariba application.</span><span class="sxs-lookup"><span data-stu-id="9ff42-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Ariba application.</span></span>

<span data-ttu-id="9ff42-152">**To configure Azure AD SSO with Ariba, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9ff42-152">**To configure Azure AD SSO with Ariba, perform the following steps:**</span></span>

1. <span data-ttu-id="9ff42-153">In the Azure classic portal, on the **Ariba** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="9ff42-153">In the Azure classic portal, on the **Ariba** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="9ff42-155">On the **How would you like users to sign on to Ariba** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-155">On the **How would you like users to sign on to Ariba** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/tutorial_ariba_03.png) 
3. <span data-ttu-id="9ff42-157">On the **Configure App Settings** dialog page, perform the following steps:.</span><span class="sxs-lookup"><span data-stu-id="9ff42-157">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/tutorial_ariba_04.png) 
  1. <span data-ttu-id="9ff42-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your Ariba application using the following pattern: **“https://<companyname>.sourcing.ariba.com"** or **"https://<CompanyName>.supplier.ariba.com”**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your Ariba application using the following pattern: **“https://<companyname>.sourcing.ariba.com"** or **"https://<CompanyName>.supplier.ariba.com”**.</span></span>
  2. <span data-ttu-id="9ff42-160">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-160">Click **Next**.</span></span>

4. <span data-ttu-id="9ff42-161">On the **Configure single sign-on at Ariba** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9ff42-161">On the **Configure single sign-on at Ariba** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/tutorial_ariba_05.png)  
  1. <span data-ttu-id="9ff42-163">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="9ff42-163">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="9ff42-164">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-164">Click **Next**.</span></span>
5. <span data-ttu-id="9ff42-165">To get SSO configured for your application, contact your Ariba support team via **1-866-218-2155**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-165">To get SSO configured for your application, contact your Ariba support team via **1-866-218-2155**.</span></span>

 >[!NOTE]
 ><span data-ttu-id="9ff42-166">Please make sure that username in the Ariba system has to match as in Azure AD otherwise the integration will not work.</span><span class="sxs-lookup"><span data-stu-id="9ff42-166">Please make sure that username in the Ariba system has to match as in Azure AD otherwise the integration will not work.</span></span>
 >  

6. <span data-ttu-id="9ff42-167">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-167">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="9ff42-169">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-169">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9ff42-171">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9ff42-171">Create an Azure AD test user</span></span>
<span data-ttu-id="9ff42-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9ff42-172">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

 ![Create Azure AD User][20]

<span data-ttu-id="9ff42-174">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9ff42-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9ff42-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-175">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="9ff42-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="9ff42-177">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="9ff42-178">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-178">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="9ff42-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-180">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="9ff42-182">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9ff42-182">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/create_aaduser_05.png)   
  1. <span data-ttu-id="9ff42-184">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="9ff42-184">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="9ff42-185">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-185">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="9ff42-186">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-186">Click **Next**.</span></span>
6. <span data-ttu-id="9ff42-187">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9ff42-187">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="9ff42-189">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-189">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="9ff42-190">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-190">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="9ff42-191">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-191">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="9ff42-192">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-192">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="9ff42-193">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-193">Click **Next**.</span></span>
7. <span data-ttu-id="9ff42-194">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-194">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="9ff42-196">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9ff42-196">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="9ff42-198">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-198">Write down the value of the **New Password**.</span></span> 
  2. <span data-ttu-id="9ff42-199">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-199">Click **Complete**.</span></span>   

### <a name="create-a-ariba-test-user"></a><span data-ttu-id="9ff42-200">Create a Ariba test user</span><span class="sxs-lookup"><span data-stu-id="9ff42-200">Create a Ariba test user</span></span>
<span data-ttu-id="9ff42-201">The objective of this section is to create a user called Britta Simon in Ariba.</span><span class="sxs-lookup"><span data-stu-id="9ff42-201">The objective of this section is to create a user called Britta Simon in Ariba.</span></span> <span data-ttu-id="9ff42-202">Please work with Ariba support team to add the users in the Ariba system.</span><span class="sxs-lookup"><span data-stu-id="9ff42-202">Please work with Ariba support team to add the users in the Ariba system.</span></span> 

 >[!NOTE]
 ><span data-ttu-id="9ff42-203">If you need to create an user manually, you need to contact the Ariba support team.</span><span class="sxs-lookup"><span data-stu-id="9ff42-203">If you need to create an user manually, you need to contact the Ariba support team.</span></span>
 >  

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="9ff42-204">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9ff42-204">Assign the Azure AD test user</span></span>
<span data-ttu-id="9ff42-205">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Ariba.</span><span class="sxs-lookup"><span data-stu-id="9ff42-205">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Ariba.</span></span>

![Assign User][200] 

<span data-ttu-id="9ff42-207">**To assign Britta Simon to Ariba, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9ff42-207">**To assign Britta Simon to Ariba, perform the following steps:**</span></span>

1. <span data-ttu-id="9ff42-208">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="9ff42-208">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="9ff42-210">In the applications list, select **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-210">In the applications list, select **Ariba**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/tutorial_ariba_50.png) 
3. <span data-ttu-id="9ff42-212">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-212">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="9ff42-214">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-214">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="9ff42-215">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="9ff42-215">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="9ff42-217">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="9ff42-217">Test single sign-on</span></span>
<span data-ttu-id="9ff42-218">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9ff42-218">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="9ff42-219">When you click the Ariba tile in the Access Panel, you should get automatically signed-on to your Ariba application.</span><span class="sxs-lookup"><span data-stu-id="9ff42-219">When you click the Ariba tile in the Access Panel, you should get automatically signed-on to your Ariba application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9ff42-220">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="9ff42-220">Additional Resources</span></span>
* [<span data-ttu-id="9ff42-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9ff42-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9ff42-222">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9ff42-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-ariba-tutorial/tutorial_general_205.png

























