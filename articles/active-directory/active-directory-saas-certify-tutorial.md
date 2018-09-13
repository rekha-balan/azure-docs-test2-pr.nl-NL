---
title: 'Tutorial: Azure Active Directory integration with Certify | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Certify.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 0b36e020-175a-4534-b341-85260739f889
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: jeedes
ms.openlocfilehash: c10ec6a1e57f4adff3633295f19751057e34a48b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555684"
---
# <a name="tutorial-azure-active-directory-integration-with-certify"></a><span data-ttu-id="11837-103">Tutorial: Azure Active Directory integration with Certify</span><span class="sxs-lookup"><span data-stu-id="11837-103">Tutorial: Azure Active Directory integration with Certify</span></span>
<span data-ttu-id="11837-104">The objective of this tutorial is to show you how to integrate Certify with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="11837-104">The objective of this tutorial is to show you how to integrate Certify with Azure Active Directory (Azure AD).</span></span>  

<span data-ttu-id="11837-105">Integrating Certify with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="11837-105">Integrating Certify with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="11837-106">You can control in Azure AD who has access to Certify</span><span class="sxs-lookup"><span data-stu-id="11837-106">You can control in Azure AD who has access to Certify</span></span>
* <span data-ttu-id="11837-107">You can enable your users to automatically get signed-on to Certify single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="11837-107">You can enable your users to automatically get signed-on to Certify single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="11837-108">You can manage your accounts in one central location - the Azure Active Directory classic portal</span><span class="sxs-lookup"><span data-stu-id="11837-108">You can manage your accounts in one central location - the Azure Active Directory classic portal</span></span>

<span data-ttu-id="11837-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="11837-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11837-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="11837-110">Prerequisites</span></span>
<span data-ttu-id="11837-111">To configure Azure AD integration with Certify, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="11837-111">To configure Azure AD integration with Certify, you need the following items:</span></span>

* <span data-ttu-id="11837-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="11837-112">An Azure AD subscription</span></span>
* <span data-ttu-id="11837-113">A Certify single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="11837-113">A Certify single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="11837-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="11837-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="11837-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="11837-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="11837-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="11837-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="11837-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="11837-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="11837-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="11837-118">Scenario Description</span></span>
<span data-ttu-id="11837-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="11837-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>  

<span data-ttu-id="11837-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="11837-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="11837-121">Adding Certify from the gallery</span><span class="sxs-lookup"><span data-stu-id="11837-121">Adding Certify from the gallery</span></span>
2. <span data-ttu-id="11837-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="11837-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-certify-from-the-gallery"></a><span data-ttu-id="11837-123">Add Certify from the gallery</span><span class="sxs-lookup"><span data-stu-id="11837-123">Add Certify from the gallery</span></span>
<span data-ttu-id="11837-124">To configure the integration of Certify into Azure AD, you need to add Certify from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="11837-124">To configure the integration of Certify into Azure AD, you need to add Certify from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="11837-125">**To add Certify from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="11837-125">**To add Certify from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="11837-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="11837-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="11837-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="11837-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="11837-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="11837-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="11837-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="11837-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="11837-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="11837-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="11837-135">In the search box, type **Certify**.</span><span class="sxs-lookup"><span data-stu-id="11837-135">In the search box, type **Certify**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/tutorial_certify_01.png)
7. <span data-ttu-id="11837-137">In the results pane, select **Certify**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="11837-137">In the results pane, select **Certify**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/tutorial_certify_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="11837-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="11837-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="11837-140">The objective of this section is to show you how to configure and test Azure AD SSO with Certify based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="11837-140">The objective of this section is to show you how to configure and test Azure AD SSO with Certify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="11837-141">For SSO to work, Azure AD needs to know what the counterpart user in Certify to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="11837-141">For SSO to work, Azure AD needs to know what the counterpart user in Certify to an user in Azure AD is.</span></span> <span data-ttu-id="11837-142">In other words, a link relationship between an Azure AD user and the related user in Certify needs to be established.</span><span class="sxs-lookup"><span data-stu-id="11837-142">In other words, a link relationship between an Azure AD user and the related user in Certify needs to be established.</span></span>  

<span data-ttu-id="11837-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Certify.</span><span class="sxs-lookup"><span data-stu-id="11837-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Certify.</span></span>

<span data-ttu-id="11837-144">To configure and test Azure AD SSO with Certify, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="11837-144">To configure and test Azure AD SSO with Certify, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="11837-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="11837-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="11837-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11837-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="11837-147">**[Creating a Certify test user](#creating-a-certify-test-user)** - to have a counterpart of Britta Simon in Certify that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="11837-147">**[Creating a Certify test user](#creating-a-certify-test-user)** - to have a counterpart of Britta Simon in Certify that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="11837-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="11837-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="11837-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="11837-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="11837-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="11837-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="11837-151">The objective of this section is to enable Azure AD SSO in the Azure AD classic portal and to configure SSO in your Certify application.</span><span class="sxs-lookup"><span data-stu-id="11837-151">The objective of this section is to enable Azure AD SSO in the Azure AD classic portal and to configure SSO in your Certify application.</span></span>

<span data-ttu-id="11837-152">**To configure Azure AD SSO with Certify, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="11837-152">**To configure Azure AD SSO with Certify, perform the following steps:**</span></span>

1. <span data-ttu-id="11837-153">In the Azure AD classic portal, on the **Certify** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="11837-153">In the Azure AD classic portal, on the **Certify** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="11837-155">On the **How would you like users to sign on to Certify** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="11837-155">On the **How would you like users to sign on to Certify** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/tutorial_certify_03.png) 
3. <span data-ttu-id="11837-157">On the **Configure App Settings** dialog page, perform the following steps:.</span><span class="sxs-lookup"><span data-stu-id="11837-157">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/tutorial_certify_04.png) 
  * <span data-ttu-id="11837-159">In the Reply URL textbox, type the Assertion Consumer Service URL using the following pattern: **“https://www.certify.com/SAML2.aspx”**.</span><span class="sxs-lookup"><span data-stu-id="11837-159">In the Reply URL textbox, type the Assertion Consumer Service URL using the following pattern: **“https://www.certify.com/SAML2.aspx”**.</span></span>

4. <span data-ttu-id="11837-160">On the **Configure single sign-on at Certify** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="11837-160">On the **Configure single sign-on at Certify** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/tutorial_certify_05.png)  
  1. <span data-ttu-id="11837-162">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="11837-162">Click **Download certificate**, and then save the file on your computer.</span></span> 
  2. <span data-ttu-id="11837-163">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="11837-163">Click **Next**.</span></span>
5. <span data-ttu-id="11837-164">To get SSO configured for your application, contact your Certify support team via support@certify.com.</span><span class="sxs-lookup"><span data-stu-id="11837-164">To get SSO configured for your application, contact your Certify support team via support@certify.com.</span></span> <span data-ttu-id="11837-165">Attach the downloaded certificate file to your mail and share the metadata urls (Entity ID, SSO Sign in URL and Sign Out URL) with Certify team to set up SSO on their side.</span><span class="sxs-lookup"><span data-stu-id="11837-165">Attach the downloaded certificate file to your mail and share the metadata urls (Entity ID, SSO Sign in URL and Sign Out URL) with Certify team to set up SSO on their side.</span></span>
6. <span data-ttu-id="11837-166">In the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="11837-166">In the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="11837-168">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="11837-168">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="11837-170">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="11837-170">Create an Azure AD test user</span></span>
<span data-ttu-id="11837-171">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11837-171">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="11837-173">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="11837-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="11837-174">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="11837-174">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="11837-176">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="11837-176">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="11837-177">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="11837-177">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="11837-179">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="11837-179">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="11837-181">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="11837-181">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="11837-183">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="11837-183">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="11837-184">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="11837-184">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="11837-185">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="11837-185">Click **Next**.</span></span>
6. <span data-ttu-id="11837-186">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="11837-186">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="11837-188">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="11837-188">In the **First Name** textbox, type **Britta**.</span></span>   
  2. <span data-ttu-id="11837-189">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="11837-189">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="11837-190">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="11837-190">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="11837-191">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="11837-191">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="11837-192">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="11837-192">Click **Next**.</span></span>
7. <span data-ttu-id="11837-193">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="11837-193">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="11837-195">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="11837-195">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="11837-197">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="11837-197">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="11837-198">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="11837-198">Click **Complete**.</span></span>   

### <a name="create-a-certify-test-user"></a><span data-ttu-id="11837-199">Create a Certify test user</span><span class="sxs-lookup"><span data-stu-id="11837-199">Create a Certify test user</span></span>
<span data-ttu-id="11837-200">The objective of this section is to create a user called Britta Simon in Certify.</span><span class="sxs-lookup"><span data-stu-id="11837-200">The objective of this section is to create a user called Britta Simon in Certify.</span></span> <span data-ttu-id="11837-201">Certify supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="11837-201">Certify supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="11837-202">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="11837-202">There is no action item for you in this section.</span></span> <span data-ttu-id="11837-203">A new user will be created during an attempt to access Certify if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="11837-203">A new user will be created during an attempt to access Certify if it doesn't exist yet.</span></span> <span data-ttu-id="11837-204">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="11837-204">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="11837-205">If you need to create an user manually, you need to contact the Certify support team.</span><span class="sxs-lookup"><span data-stu-id="11837-205">If you need to create an user manually, you need to contact the Certify support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="11837-206">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="11837-206">Assign the Azure AD test user</span></span>
<span data-ttu-id="11837-207">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Certify.</span><span class="sxs-lookup"><span data-stu-id="11837-207">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Certify.</span></span>

![Assign User][200] 

<span data-ttu-id="11837-209">**To assign Britta Simon to Certify, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="11837-209">**To assign Britta Simon to Certify, perform the following steps:**</span></span>

1. <span data-ttu-id="11837-210">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="11837-210">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="11837-212">In the applications list, select **Certify**.</span><span class="sxs-lookup"><span data-stu-id="11837-212">In the applications list, select **Certify**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/tutorial_certify_50.png) 
3. <span data-ttu-id="11837-214">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="11837-214">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="11837-216">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="11837-216">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="11837-217">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="11837-217">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="11837-219">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="11837-219">Test single sign-on</span></span>
<span data-ttu-id="11837-220">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="11837-220">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="11837-221">When you click the Certify tile in the Access Panel, you should get automatically signed-on to your Certify application.</span><span class="sxs-lookup"><span data-stu-id="11837-221">When you click the Certify tile in the Access Panel, you should get automatically signed-on to your Certify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="11837-222">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="11837-222">Additional Resources</span></span>
* [<span data-ttu-id="11837-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="11837-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="11837-224">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="11837-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-certify-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-certify-tutorial/tutorial_general_205.png

























