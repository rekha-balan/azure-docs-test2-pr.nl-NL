---
title: 'Tutorial: Azure Active Directory integration with KnowBe4 | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and KnowBe4.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: b80d2212-cc5f-4adb-836c-570640810c39
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: jeedes
ms.openlocfilehash: 9030028fda1874066f09f0f5746a07e280b2b8e2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563135"
---
# <a name="tutorial-azure-active-directory-integration-with-knowbe4"></a><span data-ttu-id="c4b2e-103">Tutorial: Azure Active Directory integration with KnowBe4</span><span class="sxs-lookup"><span data-stu-id="c4b2e-103">Tutorial: Azure Active Directory integration with KnowBe4</span></span>
<span data-ttu-id="c4b2e-104">The objective of this tutorial is to show you how to integrate KnowBe4 with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c4b2e-104">The objective of this tutorial is to show you how to integrate KnowBe4 with Azure Active Directory (Azure AD).</span></span>  

<span data-ttu-id="c4b2e-105">Integrating KnowBe4 with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="c4b2e-105">Integrating KnowBe4 with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="c4b2e-106">You can control in Azure AD who has access to KnowBe4</span><span class="sxs-lookup"><span data-stu-id="c4b2e-106">You can control in Azure AD who has access to KnowBe4</span></span>
* <span data-ttu-id="c4b2e-107">You can enable your users to automatically get signed-on to KnowBe4 single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="c4b2e-107">You can enable your users to automatically get signed-on to KnowBe4 single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="c4b2e-108">You can manage your accounts in one central location - the Azure Active Directory Portal</span><span class="sxs-lookup"><span data-stu-id="c4b2e-108">You can manage your accounts in one central location - the Azure Active Directory Portal</span></span>

<span data-ttu-id="c4b2e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c4b2e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4b2e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c4b2e-110">Prerequisites</span></span>
<span data-ttu-id="c4b2e-111">To configure Azure AD integration with KnowBe4, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="c4b2e-111">To configure Azure AD integration with KnowBe4, you need the following items:</span></span>

* <span data-ttu-id="c4b2e-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="c4b2e-112">An Azure AD subscription</span></span>
* <span data-ttu-id="c4b2e-113">A KnowBe4 single-sign (SSO) on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="c4b2e-113">A KnowBe4 single-sign (SSO) on enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="c4b2e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="c4b2e-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="c4b2e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="c4b2e-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="c4b2e-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c4b2e-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c4b2e-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="c4b2e-118">Scenario Description</span></span>
<span data-ttu-id="c4b2e-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  

<span data-ttu-id="c4b2e-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="c4b2e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="c4b2e-121">Adding KnowBe4 from the gallery</span><span class="sxs-lookup"><span data-stu-id="c4b2e-121">Adding KnowBe4 from the gallery</span></span>
* <span data-ttu-id="c4b2e-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="c4b2e-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-knowbe4-from-the-gallery"></a><span data-ttu-id="c4b2e-123">Add KnowBe4 from the gallery</span><span class="sxs-lookup"><span data-stu-id="c4b2e-123">Add KnowBe4 from the gallery</span></span>
<span data-ttu-id="c4b2e-124">To configure the integration of KnowBe4 into Azure AD, you need to add KnowBe4 from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-124">To configure the integration of KnowBe4 into Azure AD, you need to add KnowBe4 from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c4b2e-125">**To add KnowBe4 from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c4b2e-125">**To add KnowBe4 from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c4b2e-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="c4b2e-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="c4b2e-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="c4b2e-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="c4b2e-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="c4b2e-135">In the search box, type **KnowBe4**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-135">In the search box, type **KnowBe4**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/tutorial_knowbe4_01.png)
7. <span data-ttu-id="c4b2e-137">In the results pane, select **KnowBe4**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-137">In the results pane, select **KnowBe4**, and then click **Complete** to add the application.</span></span>

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c4b2e-138">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c4b2e-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="c4b2e-139">The objective of this section is to show you how to configure and test Azure AD single sign-on with KnowBe4 based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c4b2e-139">The objective of this section is to show you how to configure and test Azure AD single sign-on with KnowBe4 based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c4b2e-140">For single sign-on to work, Azure AD needs to know what the counterpart user in KnowBe4 to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-140">For single sign-on to work, Azure AD needs to know what the counterpart user in KnowBe4 to an user in Azure AD is.</span></span> <span data-ttu-id="c4b2e-141">In other words, a link relationship between an Azure AD user and the related user in KnowBe4 needs to be established.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-141">In other words, a link relationship between an Azure AD user and the related user in KnowBe4 needs to be established.</span></span>  

<span data-ttu-id="c4b2e-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in KnowBe4.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in KnowBe4.</span></span>

<span data-ttu-id="c4b2e-143">To configure and test Azure AD single sign-on with KnowBe4, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c4b2e-143">To configure and test Azure AD single sign-on with KnowBe4, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c4b2e-144">**[Configure Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-144">**[Configure Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c4b2e-145">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-145">**[Create an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c4b2e-146">**[Create a KnowBe4 test user](#creating-a-KnowBe4-test-user)** - to have a counterpart of Britta Simon in KnowBe4 that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-146">**[Create a KnowBe4 test user](#creating-a-KnowBe4-test-user)** - to have a counterpart of Britta Simon in KnowBe4 that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="c4b2e-147">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-147">**[Assign the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c4b2e-148">**[Test single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-148">**[Test single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c4b2e-149">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="c4b2e-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="c4b2e-150">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your KnowBe4 application.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-150">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your KnowBe4 application.</span></span>

<span data-ttu-id="c4b2e-151">**To configure Azure AD single sign-on with KnowBe4, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c4b2e-151">**To configure Azure AD single sign-on with KnowBe4, perform the following steps:**</span></span>

1. <span data-ttu-id="c4b2e-152">In the Azure classic portal, on the **KnowBe4** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-152">In the Azure classic portal, on the **KnowBe4** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="c4b2e-154">On the **How would you like users to sign on to KnowBe4** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-154">On the **How would you like users to sign on to KnowBe4** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/tutorial_knowbe4_03.png) 
3. <span data-ttu-id="c4b2e-156">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c4b2e-156">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/tutorial_knowbe4_04.png) 

  * <span data-ttu-id="c4b2e-158">In the Sign On URL textbox, type the URL used by your users to sign-on to your KnowBe4 application using the following pattern: **“https://\<company name\>.knowbe4.com/auth/saml/aad168.ccsctp.net)”**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-158">In the Sign On URL textbox, type the URL used by your users to sign-on to your KnowBe4 application using the following pattern: **“https://\<company name\>.knowbe4.com/auth/saml/aad168.ccsctp.net)”**.</span></span>

4. <span data-ttu-id="c4b2e-159">On the **Configure single sign-on at KnowBe4** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c4b2e-159">On the **Configure single sign-on at KnowBe4** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/tutorial_knowbe4_05.png) 
   
   1. <span data-ttu-id="c4b2e-161">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-161">Click **Download certificate**, and then save the file on your computer.</span></span> 
   2. <span data-ttu-id="c4b2e-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-162">Click **Next**.</span></span>
5. <span data-ttu-id="c4b2e-163">To get SSO configured for your application, contact your [KnowBe4 support team](mailto:support@knowbe4.com).</span><span class="sxs-lookup"><span data-stu-id="c4b2e-163">To get SSO configured for your application, contact your [KnowBe4 support team](mailto:support@knowbe4.com).</span></span> <span data-ttu-id="c4b2e-164">Attach the downloaded certificate file to your mail and share the metadata urls (Entity ID, SSO Sign in URL and Sign Out URL) with KnowBe4 team to set up SSO on their side.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-164">Attach the downloaded certificate file to your mail and share the metadata urls (Entity ID, SSO Sign in URL and Sign Out URL) with KnowBe4 team to set up SSO on their side.</span></span>
6. <span data-ttu-id="c4b2e-165">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-165">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="c4b2e-167">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-167">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c4b2e-169">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c4b2e-169">Create an Azure AD test user</span></span>
<span data-ttu-id="c4b2e-170">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-170">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Create Azure AD User][20]

<span data-ttu-id="c4b2e-172">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c4b2e-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c4b2e-173">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-173">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="c4b2e-175">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-175">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="c4b2e-176">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-176">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="c4b2e-178">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-178">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="c4b2e-180">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c4b2e-180">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/create_aaduser_05.png) 
   
   1. <span data-ttu-id="c4b2e-182">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-182">As Type Of User, select New user in your organization.</span></span>   
   2. <span data-ttu-id="c4b2e-183">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-183">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   3. <span data-ttu-id="c4b2e-184">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-184">Click **Next**.</span></span>
6. <span data-ttu-id="c4b2e-185">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c4b2e-185">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/create_aaduser_06.png) 
   
   1. <span data-ttu-id="c4b2e-187">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-187">In the **First Name** textbox, type **Britta**.</span></span>  
   2. <span data-ttu-id="c4b2e-188">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-188">In the **Last Name** textbox, type, **Simon**.</span></span>
   3. <span data-ttu-id="c4b2e-189">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-189">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   4. <span data-ttu-id="c4b2e-190">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-190">In the **Role** list, select **User**.</span></span>
   5. <span data-ttu-id="c4b2e-191">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-191">Click **Next**.</span></span>
7. <span data-ttu-id="c4b2e-192">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-192">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="c4b2e-194">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c4b2e-194">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/create_aaduser_08.png) 
   
    1. <span data-ttu-id="c4b2e-196">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-196">Write down the value of the **New Password**.</span></span>
    2. <span data-ttu-id="c4b2e-197">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-197">Click **Complete**.</span></span>   

### <a name="create-a-knowbe4-test-user"></a><span data-ttu-id="c4b2e-198">Create a KnowBe4 test user</span><span class="sxs-lookup"><span data-stu-id="c4b2e-198">Create a KnowBe4 test user</span></span>
<span data-ttu-id="c4b2e-199">The objective of this section is to create a user called Britta Simon in KnowBe4.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-199">The objective of this section is to create a user called Britta Simon in KnowBe4.</span></span> <span data-ttu-id="c4b2e-200">KnowBe4 supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-200">KnowBe4 supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="c4b2e-201">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-201">There is no action item for you in this section.</span></span> <span data-ttu-id="c4b2e-202">A new user will be created during an attempt to access KnowBe4 if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-202">A new user will be created during an attempt to access KnowBe4 if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="c4b2e-203">If you need to create an user manually, you need to contact the KnowBe4 support team.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-203">If you need to create an user manually, you need to contact the KnowBe4 support team.</span></span>
>  

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c4b2e-204">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c4b2e-204">Assign the Azure AD test user</span></span>
<span data-ttu-id="c4b2e-205">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to KnowBe4.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-205">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to KnowBe4.</span></span>

   ![Assign User][200] 

<span data-ttu-id="c4b2e-207">**To assign Britta Simon to KnowBe4, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c4b2e-207">**To assign Britta Simon to KnowBe4, perform the following steps:**</span></span>

1. <span data-ttu-id="c4b2e-208">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-208">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="c4b2e-210">In the applications list, select **KnowBe4**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-210">In the applications list, select **KnowBe4**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/tutorial_knowbe4_50.png) 
3. <span data-ttu-id="c4b2e-212">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-212">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="c4b2e-214">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-214">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="c4b2e-215">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-215">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="c4b2e-217">Test Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="c4b2e-217">Test Single Sign-On</span></span>
<span data-ttu-id="c4b2e-218">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-218">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="c4b2e-219">When you click the KnowBe4 tile in the Access Panel, you should get automatically signed-on to your KnowBe4 application.</span><span class="sxs-lookup"><span data-stu-id="c4b2e-219">When you click the KnowBe4 tile in the Access Panel, you should get automatically signed-on to your KnowBe4 application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c4b2e-220">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="c4b2e-220">Additional Resources</span></span>
* [<span data-ttu-id="c4b2e-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c4b2e-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c4b2e-222">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c4b2e-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-knowbe4-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-knowbe4-tutorial/tutorial_general_205.png
























