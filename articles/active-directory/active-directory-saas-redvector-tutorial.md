---
title: 'Tutorial: Azure Active Directory integration with RedVector | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and RedVector.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 99042f39-0ab2-475b-8df8-3016d7f875e9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: jeedes
ms.openlocfilehash: c1f10f9515ecb43da53fac4a7ae1c28ddaad4d86
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556599"
---
# <a name="tutorial-azure-active-directory-integration-with-redvector"></a><span data-ttu-id="36621-103">Tutorial: Azure Active Directory integration with RedVector</span><span class="sxs-lookup"><span data-stu-id="36621-103">Tutorial: Azure Active Directory integration with RedVector</span></span>
<span data-ttu-id="36621-104">In this tutorial, you learn how to integrate RedVector with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="36621-104">In this tutorial, you learn how to integrate RedVector with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="36621-105">Integrating RedVector with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="36621-105">Integrating RedVector with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="36621-106">You can control in Azure AD who has access to RedVector</span><span class="sxs-lookup"><span data-stu-id="36621-106">You can control in Azure AD who has access to RedVector</span></span>
* <span data-ttu-id="36621-107">You can enable your users to automatically get signed-on to RedVector single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="36621-107">You can enable your users to automatically get signed-on to RedVector single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="36621-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="36621-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="36621-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="36621-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36621-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="36621-110">Prerequisites</span></span>
<span data-ttu-id="36621-111">To configure Azure AD integration with RedVector, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="36621-111">To configure Azure AD integration with RedVector, you need the following items:</span></span>

* <span data-ttu-id="36621-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="36621-112">An Azure AD subscription</span></span>
* <span data-ttu-id="36621-113">A **RedVector** single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="36621-113">A **RedVector** single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="36621-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="36621-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>  

<span data-ttu-id="36621-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="36621-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="36621-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="36621-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="36621-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="36621-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="36621-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="36621-118">Scenario description</span></span>
<span data-ttu-id="36621-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="36621-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="36621-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="36621-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="36621-121">Adding RedVector from the gallery</span><span class="sxs-lookup"><span data-stu-id="36621-121">Adding RedVector from the gallery</span></span>
2. <span data-ttu-id="36621-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="36621-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="add-redvector-from-the-gallery"></a><span data-ttu-id="36621-123">Add RedVector from the gallery</span><span class="sxs-lookup"><span data-stu-id="36621-123">Add RedVector from the gallery</span></span>
<span data-ttu-id="36621-124">To configure the integration of RedVector into Azure AD, you need to add RedVector from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="36621-124">To configure the integration of RedVector into Azure AD, you need to add RedVector from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="36621-125">**To add RedVector from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="36621-125">**To add RedVector from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="36621-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="36621-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="36621-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="36621-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="36621-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="36621-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="36621-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="36621-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="36621-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="36621-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="36621-135">In the search box, type **RedVector**.</span><span class="sxs-lookup"><span data-stu-id="36621-135">In the search box, type **RedVector**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/tutorial_redvector_01.png)
7. <span data-ttu-id="36621-137">In the results pane, select **RedVector**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="36621-137">In the results pane, select **RedVector**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/tutorial_redvector_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="36621-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="36621-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="36621-140">In this section, you configure and test Azure AD SSO with RedVector based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="36621-140">In this section, you configure and test Azure AD SSO with RedVector based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="36621-141">For SSO to work, Azure AD needs to know what the counterpart user in RedVector is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36621-141">For SSO to work, Azure AD needs to know what the counterpart user in RedVector is to a user in Azure AD.</span></span> <span data-ttu-id="36621-142">In other words, a link relationship between an Azure AD user and the related user in RedVector needs to be established.</span><span class="sxs-lookup"><span data-stu-id="36621-142">In other words, a link relationship between an Azure AD user and the related user in RedVector needs to be established.</span></span>

<span data-ttu-id="36621-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in RedVector.</span><span class="sxs-lookup"><span data-stu-id="36621-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in RedVector.</span></span>

<span data-ttu-id="36621-144">To configure and test Azure AD single sign-on with RedVector, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="36621-144">To configure and test Azure AD single sign-on with RedVector, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="36621-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="36621-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="36621-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="36621-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="36621-147">**[Creating a RedVector test user](#creating-a-RedVector-test-user)** - to have a counterpart of Britta Simon in RedVector that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="36621-147">**[Creating a RedVector test user](#creating-a-RedVector-test-user)** - to have a counterpart of Britta Simon in RedVector that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="36621-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="36621-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="36621-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="36621-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="36621-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="36621-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="36621-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your RedVector application.</span><span class="sxs-lookup"><span data-stu-id="36621-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your RedVector application.</span></span>

<span data-ttu-id="36621-152">**To configure Azure AD SSO with RedVector, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="36621-152">**To configure Azure AD SSO with RedVector, perform the following steps:**</span></span>

1. <span data-ttu-id="36621-153">In the menu on the top, click **Quick Start**.</span><span class="sxs-lookup"><span data-stu-id="36621-153">In the menu on the top, click **Quick Start**.</span></span>
   
    ![Configure Single Sign-On][6]
2. <span data-ttu-id="36621-155">In the classic portal, on the **RedVector** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="36621-155">In the classic portal, on the **RedVector** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][7] 
3. <span data-ttu-id="36621-157">On the **How would you like users to sign on to RedVector** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="36621-157">On the **How would you like users to sign on to RedVector** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/tutorial_redvector_06.png)
4. <span data-ttu-id="36621-159">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="36621-159">On the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/tutorial_redvector_07.png)
 1. <span data-ttu-id="36621-161">In the Sign On URL text box, type a URL using the following pattern: `https://sso2.redvector.com/adfs/<Companyname>`.</span><span class="sxs-lookup"><span data-stu-id="36621-161">In the Sign On URL text box, type a URL using the following pattern: `https://sso2.redvector.com/adfs/<Companyname>`.</span></span> <span data-ttu-id="36621-162">You may have to contact Redvector support at <sso@redvector.com> to get the correct values for your environment.</span><span class="sxs-lookup"><span data-stu-id="36621-162">You may have to contact Redvector support at <sso@redvector.com> to get the correct values for your environment.</span></span>
 2. <span data-ttu-id="36621-163">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="36621-163">Click **Next**.</span></span>

5. <span data-ttu-id="36621-164">On the **Configure single sign-on at RedVector** page, Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="36621-164">On the **Configure single sign-on at RedVector** page, Click **Download certificate**, and then save the file on your computer.</span></span> <span data-ttu-id="36621-165">Also, copy the single sign-on service URL value.</span><span class="sxs-lookup"><span data-stu-id="36621-165">Also, copy the single sign-on service URL value.</span></span> <span data-ttu-id="36621-166">You will need to share this information with RedVector support to get SSO configured.</span><span class="sxs-lookup"><span data-stu-id="36621-166">You will need to share this information with RedVector support to get SSO configured.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/tutorial_redvector_08.png)
6. <span data-ttu-id="36621-168">To get SSO configured for your application, contact RedVector support team at <mailto:sso@redvector.com>.</span><span class="sxs-lookup"><span data-stu-id="36621-168">To get SSO configured for your application, contact RedVector support team at <mailto:sso@redvector.com>.</span></span> <span data-ttu-id="36621-169">They will assist with the proper channel to configure SSO.</span><span class="sxs-lookup"><span data-stu-id="36621-169">They will assist with the proper channel to configure SSO.</span></span> <span data-ttu-id="36621-170">In the email, provide them the following:</span><span class="sxs-lookup"><span data-stu-id="36621-170">In the email, provide them the following:</span></span> 
   * <span data-ttu-id="36621-171">The downloaded certificate</span><span class="sxs-lookup"><span data-stu-id="36621-171">The downloaded certificate</span></span>
   * <span data-ttu-id="36621-172">The **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="36621-172">The **SAML SSO URL**</span></span>
6. <span data-ttu-id="36621-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="36621-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="36621-175">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="36621-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="36621-177">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="36621-177">Create an Azure AD test user</span></span>
<span data-ttu-id="36621-178">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="36621-178">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="36621-180">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="36621-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="36621-181">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="36621-181">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="36621-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="36621-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="36621-184">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="36621-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="36621-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="36621-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="36621-188">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="36621-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="36621-190">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="36621-190">As Type Of User, select New user in your organization.</span></span> 
  2. <span data-ttu-id="36621-191">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="36621-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="36621-192">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="36621-192">Click **Next**.</span></span>
6. <span data-ttu-id="36621-193">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="36621-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="36621-195">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="36621-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="36621-196">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="36621-196">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="36621-197">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="36621-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="36621-198">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="36621-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="36621-199">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="36621-199">Click **Next**.</span></span>
7. <span data-ttu-id="36621-200">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="36621-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="36621-202">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="36621-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="36621-204">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="36621-204">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="36621-205">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="36621-205">Click **Complete**.</span></span>   

### <a name="create-a-redvector-test-user"></a><span data-ttu-id="36621-206">Create a RedVector test user</span><span class="sxs-lookup"><span data-stu-id="36621-206">Create a RedVector test user</span></span>
<span data-ttu-id="36621-207">In this section, you create a user called Britta Simon in RedVector.</span><span class="sxs-lookup"><span data-stu-id="36621-207">In this section, you create a user called Britta Simon in RedVector.</span></span> <span data-ttu-id="36621-208">If you don't know how to add Britta Simon in RedVector, please work with RedVector support team to add the test user and enable SSO.</span><span class="sxs-lookup"><span data-stu-id="36621-208">If you don't know how to add Britta Simon in RedVector, please work with RedVector support team to add the test user and enable SSO.</span></span> <span data-ttu-id="36621-209">Contact them at <mailto:sso@redvector.com>.</span><span class="sxs-lookup"><span data-stu-id="36621-209">Contact them at <mailto:sso@redvector.com>.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="36621-210">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="36621-210">Assign the Azure AD test user</span></span>
<span data-ttu-id="36621-211">In this section, you enable Britta Simon to use Azure SSO by granting her access to RedVector.</span><span class="sxs-lookup"><span data-stu-id="36621-211">In this section, you enable Britta Simon to use Azure SSO by granting her access to RedVector.</span></span>

![Assign User][200] 

<span data-ttu-id="36621-213">**To assign Britta Simon to RedVector, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="36621-213">**To assign Britta Simon to RedVector, perform the following steps:**</span></span>

1. <span data-ttu-id="36621-214">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="36621-214">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="36621-216">In the applications list, select **RedVector**.</span><span class="sxs-lookup"><span data-stu-id="36621-216">In the applications list, select **RedVector**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/tutorial_redvector_09.png) 
3. <span data-ttu-id="36621-218">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="36621-218">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="36621-220">In the All Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="36621-220">In the All Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="36621-221">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="36621-221">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="36621-223">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="36621-223">Test single sign-on</span></span>
<span data-ttu-id="36621-224">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="36621-224">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="36621-225">When you click the RedVector tile in the Access Panel, you should get automatically signed-on to your RedVector application.</span><span class="sxs-lookup"><span data-stu-id="36621-225">When you click the RedVector tile in the Access Panel, you should get automatically signed-on to your RedVector application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="36621-226">Additional resources</span><span class="sxs-lookup"><span data-stu-id="36621-226">Additional resources</span></span>
* [<span data-ttu-id="36621-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="36621-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="36621-228">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="36621-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/tutorial_general_04.png


[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/tutorial_general_05.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/tutorial_general_06.png
[7]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/tutorial_general_050.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/tutorial_general_060.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/tutorial_general_070.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-redvector-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-redvector-tutorial/tutorial_general_205.png



























