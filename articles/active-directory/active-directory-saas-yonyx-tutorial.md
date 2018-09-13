---
title: 'Tutorial: Azure Active Directory integration with Yonyx Interactive Guides | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Yonyx Interactive Guides.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 07db4e01-319b-4cb6-9b93-4577bffd3cbc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2017
ms.author: jeedes
ms.openlocfilehash: f2aa34ae8853b5d2facbac43bcfbe41403be84d5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554539"
---
# <a name="tutorial-azure-active-directory-integration-with-yonyx-interactive-guides"></a><span data-ttu-id="1825f-103">Tutorial: Azure Active Directory integration with Yonyx Interactive Guides</span><span class="sxs-lookup"><span data-stu-id="1825f-103">Tutorial: Azure Active Directory integration with Yonyx Interactive Guides</span></span>
<span data-ttu-id="1825f-104">The objective of this tutorial is to show you how to integrate Yonyx Interactive Guides with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1825f-104">The objective of this tutorial is to show you how to integrate Yonyx Interactive Guides with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1825f-105">Integrating Yonyx Interactive Guides with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1825f-105">Integrating Yonyx Interactive Guides with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="1825f-106">You can control in Azure AD who has access to Yonyx Interactive Guides</span><span class="sxs-lookup"><span data-stu-id="1825f-106">You can control in Azure AD who has access to Yonyx Interactive Guides</span></span>
* <span data-ttu-id="1825f-107">You can enable your users to automatically get signed-on to Yonyx Interactive Guides single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="1825f-107">You can enable your users to automatically get signed-on to Yonyx Interactive Guides single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="1825f-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="1825f-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="1825f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1825f-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1825f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1825f-110">Prerequisites</span></span>
<span data-ttu-id="1825f-111">To configure Azure AD integration with Yonyx Interactive Guides, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1825f-111">To configure Azure AD integration with Yonyx Interactive Guides, you need the following items:</span></span>

* <span data-ttu-id="1825f-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="1825f-112">An Azure AD subscription</span></span>
* <span data-ttu-id="1825f-113">A Yonyx Interactive Guides SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1825f-113">A Yonyx Interactive Guides SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="1825f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1825f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="1825f-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1825f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="1825f-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="1825f-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="1825f-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1825f-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1825f-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="1825f-118">Scenario description</span></span>
<span data-ttu-id="1825f-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1825f-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="1825f-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1825f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1825f-121">Adding Yonyx Interactive Guides from the gallery</span><span class="sxs-lookup"><span data-stu-id="1825f-121">Adding Yonyx Interactive Guides from the gallery</span></span>
2. <span data-ttu-id="1825f-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="1825f-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-yonyx-interactive-guides-from-the-gallery"></a><span data-ttu-id="1825f-123">Adding Yonyx Interactive Guides from the gallery</span><span class="sxs-lookup"><span data-stu-id="1825f-123">Adding Yonyx Interactive Guides from the gallery</span></span>
<span data-ttu-id="1825f-124">To configure the integration of Yonyx Interactive Guides into Azure AD, you need to add Yonyx Interactive Guides from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1825f-124">To configure the integration of Yonyx Interactive Guides into Azure AD, you need to add Yonyx Interactive Guides from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1825f-125">**To add Yonyx Interactive Guides from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1825f-125">**To add Yonyx Interactive Guides from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1825f-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1825f-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="1825f-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1825f-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1825f-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1825f-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="1825f-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1825f-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="1825f-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="1825f-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="1825f-135">In the search box, type **Yonyx Interactive Guides**.</span><span class="sxs-lookup"><span data-stu-id="1825f-135">In the search box, type **Yonyx Interactive Guides**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/tutorial_yonyx_01.png)
7. <span data-ttu-id="1825f-137">In the results panel, select **Yonyx Interactive Guides**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="1825f-137">In the results panel, select **Yonyx Interactive Guides**, and then click **Complete** to add the application.</span></span>
   
    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/tutorial_yonyx_0001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="1825f-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="1825f-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="1825f-140">The objective of this section is to show you how to configure and test Azure AD SSO with Yonyx Interactive Guides based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1825f-140">The objective of this section is to show you how to configure and test Azure AD SSO with Yonyx Interactive Guides based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1825f-141">For SSO to work, Azure AD needs to know what the counterpart user in Yonyx Interactive Guides to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="1825f-141">For SSO to work, Azure AD needs to know what the counterpart user in Yonyx Interactive Guides to an user in Azure AD is.</span></span> <span data-ttu-id="1825f-142">In other words, a link relationship between an Azure AD user and the related user in Yonyx Interactive Guides needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1825f-142">In other words, a link relationship between an Azure AD user and the related user in Yonyx Interactive Guides needs to be established.</span></span>

<span data-ttu-id="1825f-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Yonyx Interactive Guides.</span><span class="sxs-lookup"><span data-stu-id="1825f-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Yonyx Interactive Guides.</span></span>

<span data-ttu-id="1825f-144">To configure and test Azure AD SSO with Yonyx Interactive Guides, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1825f-144">To configure and test Azure AD SSO with Yonyx Interactive Guides, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1825f-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1825f-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1825f-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1825f-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1825f-147">**[Creating a Yonyx Interactive Guides test user](#creating-a-yonyx-interactive-guides-test-user)** - to have a counterpart of Britta Simon in Yonyx Interactive Guides that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="1825f-147">**[Creating a Yonyx Interactive Guides test user](#creating-a-yonyx-interactive-guides-test-user)** - to have a counterpart of Britta Simon in Yonyx Interactive Guides that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="1825f-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1825f-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1825f-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1825f-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="1825f-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="1825f-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="1825f-151">In this section, you enable Azure AD SSO in the classic portal and configure single sign-on in your Yonyx Interactive Guides application.</span><span class="sxs-lookup"><span data-stu-id="1825f-151">In this section, you enable Azure AD SSO in the classic portal and configure single sign-on in your Yonyx Interactive Guides application.</span></span>

<span data-ttu-id="1825f-152">**To configure Azure AD SSO with Yonyx Interactive Guides, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1825f-152">**To configure Azure AD SSO with Yonyx Interactive Guides, perform the following steps:**</span></span>

1. <span data-ttu-id="1825f-153">In the classic portal, on the **Yonyx Interactive Guides** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="1825f-153">In the classic portal, on the **Yonyx Interactive Guides** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="1825f-155">On the **How would you like users to sign on to Yonyx Interactive Guides** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1825f-155">On the **How would you like users to sign on to Yonyx Interactive Guides** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/tutorial_yonyx_03.png)
3. <span data-ttu-id="1825f-157">On the **Configure App Settings** dialog page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="1825f-157">On the **Configure App Settings** dialog page, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/tutorial_yonyx_04.png)
  1. <span data-ttu-id="1825f-159">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.yonyx.com/y/conversation/?id=<guid number>`.</span><span class="sxs-lookup"><span data-stu-id="1825f-159">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.yonyx.com/y/conversation/?id=<guid number>`.</span></span> 
  2. <span data-ttu-id="1825f-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.yonyx.com`.</span><span class="sxs-lookup"><span data-stu-id="1825f-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.yonyx.com`.</span></span>
  3. <span data-ttu-id="1825f-161">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1825f-161">Click **Next**.</span></span>
   
    >[!NOTE]
    > <span data-ttu-id="1825f-162">Please note that you have to update these values with the actual Sign On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="1825f-162">Please note that you have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="1825f-163">To get these values, contact Yonyx Interactive Guides support team via <mailto:support@yonyx.com>.</span><span class="sxs-lookup"><span data-stu-id="1825f-163">To get these values, contact Yonyx Interactive Guides support team via <mailto:support@yonyx.com>.</span></span> 
    > 
4. <span data-ttu-id="1825f-164">On the **Configure single sign-on at Yonyx Interactive Guides** page, click **Download certificate** and then save the file on your computer:</span><span class="sxs-lookup"><span data-stu-id="1825f-164">On the **Configure single sign-on at Yonyx Interactive Guides** page, click **Download certificate** and then save the file on your computer:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/tutorial_yonyx_05.png)
5. <span data-ttu-id="1825f-166">To get SSO configured for your application, contact Yonyx Interactive Guides support team via <mailto:support@yonyx.com> and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="1825f-166">To get SSO configured for your application, contact Yonyx Interactive Guides support team via <mailto:support@yonyx.com> and provide them with the following:</span></span>
  * <span data-ttu-id="1825f-167">The downloaded **Certificate**</span><span class="sxs-lookup"><span data-stu-id="1825f-167">The downloaded **Certificate**</span></span>
  * <span data-ttu-id="1825f-168">The **Issuer URL**</span><span class="sxs-lookup"><span data-stu-id="1825f-168">The **Issuer URL**</span></span>
  * <span data-ttu-id="1825f-169">The **Single Sign-On Service URL**</span><span class="sxs-lookup"><span data-stu-id="1825f-169">The **Single Sign-On Service URL**</span></span>
  * <span data-ttu-id="1825f-170">The **Single Sign-Out Service URL**</span><span class="sxs-lookup"><span data-stu-id="1825f-170">The **Single Sign-Out Service URL**</span></span>
6. <span data-ttu-id="1825f-171">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1825f-171">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="1825f-173">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1825f-173">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1825f-175">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1825f-175">Create an Azure AD test user</span></span>
<span data-ttu-id="1825f-176">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1825f-176">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="1825f-178">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1825f-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1825f-179">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1825f-179">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="1825f-181">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1825f-181">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1825f-182">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="1825f-182">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="1825f-184">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="1825f-184">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="1825f-186">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1825f-186">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/create_aaduser_05.png) 
 1. <span data-ttu-id="1825f-188">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="1825f-188">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="1825f-189">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1825f-189">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="1825f-190">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1825f-190">Click **Next**.</span></span>
6. <span data-ttu-id="1825f-191">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1825f-191">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/create_aaduser_06.png) 
 1. <span data-ttu-id="1825f-193">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1825f-193">In the **First Name** textbox, type **Britta**.</span></span>   
 2. <span data-ttu-id="1825f-194">In the **Last Name** textbox, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1825f-194">In the **Last Name** textbox, type **Simon**.</span></span> 
 3. <span data-ttu-id="1825f-195">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1825f-195">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="1825f-196">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="1825f-196">In the **Role** list, select **User**.</span></span> 
 5. <span data-ttu-id="1825f-197">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1825f-197">Click **Next**.</span></span>
7. <span data-ttu-id="1825f-198">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="1825f-198">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="1825f-200">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1825f-200">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/create_aaduser_08.png) 
 1. <span data-ttu-id="1825f-202">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="1825f-202">Write down the value of the **New Password**.</span></span>
 2. <span data-ttu-id="1825f-203">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1825f-203">Click **Complete**.</span></span>   

### <a name="create-a-yonyx-interactive-guides-test-user"></a><span data-ttu-id="1825f-204">Create a Yonyx Interactive Guides test user</span><span class="sxs-lookup"><span data-stu-id="1825f-204">Create a Yonyx Interactive Guides test user</span></span>
<span data-ttu-id="1825f-205">The objective of this section is to create a user called Britta Simon in Yonyx Interactive Guides.</span><span class="sxs-lookup"><span data-stu-id="1825f-205">The objective of this section is to create a user called Britta Simon in Yonyx Interactive Guides.</span></span> <span data-ttu-id="1825f-206">Yonyx Interactive Guides supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="1825f-206">Yonyx Interactive Guides supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="1825f-207">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="1825f-207">There is no action item for you in this section.</span></span> <span data-ttu-id="1825f-208">A new user will be created during an attempt to access Adobe Creative Cloud if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="1825f-208">A new user will be created during an attempt to access Adobe Creative Cloud if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="1825f-209">If you need to create an user manually, you need to contact the Yonyx Interactive Guides support team via <mailto:support@yonyx.com>.</span><span class="sxs-lookup"><span data-stu-id="1825f-209">If you need to create an user manually, you need to contact the Yonyx Interactive Guides support team via <mailto:support@yonyx.com>.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1825f-210">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1825f-210">Assign the Azure AD test user</span></span>
<span data-ttu-id="1825f-211">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Yonyx Interactive Guides.</span><span class="sxs-lookup"><span data-stu-id="1825f-211">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Yonyx Interactive Guides.</span></span>

![Assign User][200]

<span data-ttu-id="1825f-213">**To assign Britta Simon to Yonyx Interactive Guides, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1825f-213">**To assign Britta Simon to Yonyx Interactive Guides, perform the following steps:**</span></span>

1. <span data-ttu-id="1825f-214">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1825f-214">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201]
2. <span data-ttu-id="1825f-216">In the applications list, select **Yonyx Interactive Guides**.</span><span class="sxs-lookup"><span data-stu-id="1825f-216">In the applications list, select **Yonyx Interactive Guides**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/tutorial_yonyx_50.png)
3. <span data-ttu-id="1825f-218">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="1825f-218">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="1825f-220">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1825f-220">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="1825f-221">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="1825f-221">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="1825f-223">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="1825f-223">Test single sign-on</span></span>
<span data-ttu-id="1825f-224">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1825f-224">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1825f-225">When you click the Yonyx Interactive Guides tile in the Access Panel, you should get automatically signed-on to your Yonyx Interactive Guides application.</span><span class="sxs-lookup"><span data-stu-id="1825f-225">When you click the Yonyx Interactive Guides tile in the Access Panel, you should get automatically signed-on to your Yonyx Interactive Guides application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1825f-226">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1825f-226">Additional resources</span></span>
* [<span data-ttu-id="1825f-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1825f-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1825f-228">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1825f-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-yonyx-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-yonyx-tutorial/tutorial_general_205.png

























