---
title: 'Tutorial: Azure Active Directory integration with 8x8 Virtual Office | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and 8x8 Virtual Office.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: b34a6edf-e745-4aec-b0b2-7337473d64c5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: 28f90473458138c57e1290174011649c38c55045
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550284"
---
# <a name="tutorial-azure-active-directory-integration-with-8x8-virtual-office"></a><span data-ttu-id="e18df-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="e18df-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span></span>
<span data-ttu-id="e18df-104">The objective of this tutorial is to show you how to integrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e18df-104">The objective of this tutorial is to show you how to integrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e18df-105">Integrating 8x8 Virtual Office with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="e18df-105">Integrating 8x8 Virtual Office with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="e18df-106">You can control in Azure AD who has access to 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="e18df-106">You can control in Azure AD who has access to 8x8 Virtual Office</span></span>
* <span data-ttu-id="e18df-107">You can enable your users to automatically get signed-on to 8x8 Virtual Office single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="e18df-107">You can enable your users to automatically get signed-on to 8x8 Virtual Office single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="e18df-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="e18df-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="e18df-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e18df-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e18df-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e18df-110">Prerequisites</span></span>
<span data-ttu-id="e18df-111">To configure Azure AD integration with 8x8 Virtual Office, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="e18df-111">To configure Azure AD integration with 8x8 Virtual Office, you need the following items:</span></span>

* <span data-ttu-id="e18df-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="e18df-112">An Azure AD subscription</span></span>
* <span data-ttu-id="e18df-113">A 8x8 Virtual Office single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="e18df-113">A 8x8 Virtual Office single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="e18df-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="e18df-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

    To test the steps in this tutorial, you should follow these recommendations:

* <span data-ttu-id="e18df-115">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="e18df-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="e18df-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e18df-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e18df-117">Scenario description</span><span class="sxs-lookup"><span data-stu-id="e18df-117">Scenario description</span></span>
<span data-ttu-id="e18df-118">The objective of this tutorial is to enable you to test Microsoft Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="e18df-118">The objective of this tutorial is to enable you to test Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="e18df-119">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="e18df-119">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e18df-120">Adding 8x8 Virtual Office from the gallery</span><span class="sxs-lookup"><span data-stu-id="e18df-120">Adding 8x8 Virtual Office from the gallery</span></span>
2. <span data-ttu-id="e18df-121">Configuring and testing Microsoft Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="e18df-121">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="adding-8x8-virtual-office-from-the-gallery"></a><span data-ttu-id="e18df-122">Adding 8x8 Virtual Office from the gallery</span><span class="sxs-lookup"><span data-stu-id="e18df-122">Adding 8x8 Virtual Office from the gallery</span></span>
<span data-ttu-id="e18df-123">To configure the integration of 8x8 Virtual Office into Azure AD, you need to add 8x8 Virtual Office from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="e18df-123">To configure the integration of 8x8 Virtual Office into Azure AD, you need to add 8x8 Virtual Office from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e18df-124">**To add 8x8 Virtual Office from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e18df-124">**To add 8x8 Virtual Office from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e18df-125">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e18df-125">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="e18df-127">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="e18df-127">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="e18df-128">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="e18df-128">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="e18df-130">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="e18df-130">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="e18df-132">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="e18df-132">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="e18df-134">In the search box, type **8x8 Virtual Office**.</span><span class="sxs-lookup"><span data-stu-id="e18df-134">In the search box, type **8x8 Virtual Office**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_01.png)
7. <span data-ttu-id="e18df-136">In the results pane, select **8x8 Virtual Office**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="e18df-136">In the results pane, select **8x8 Virtual Office**, and then click **Complete** to add the application.</span></span>
   
    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_0001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="e18df-138">Configure and test Microsoft Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="e18df-138">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="e18df-139">The objective of this section is to show you how to configure and test Microsoft Azure AD SSO with 8x8 Virtual Office based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e18df-139">The objective of this section is to show you how to configure and test Microsoft Azure AD SSO with 8x8 Virtual Office based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e18df-140">For SSO to work, Azure AD needs to know what the counterpart user in 8x8 Virtual Office to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="e18df-140">For SSO to work, Azure AD needs to know what the counterpart user in 8x8 Virtual Office to an user in Azure AD is.</span></span> <span data-ttu-id="e18df-141">In other words, a link relationship between an Azure AD user and the related user in 8x8 Virtual Office needs to be established.</span><span class="sxs-lookup"><span data-stu-id="e18df-141">In other words, a link relationship between an Azure AD user and the related user in 8x8 Virtual Office needs to be established.</span></span>

<span data-ttu-id="e18df-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="e18df-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in 8x8 Virtual Office.</span></span>

<span data-ttu-id="e18df-143">To configure and test Microsoft Azure AD SSO with 8x8 Virtual Office, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e18df-143">To configure and test Microsoft Azure AD SSO with 8x8 Virtual Office, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e18df-144">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="e18df-144">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e18df-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e18df-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="e18df-146">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - to have a counterpart of Britta Simon in 8x8 Virtual Office that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="e18df-146">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - to have a counterpart of Britta Simon in 8x8 Virtual Office that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="e18df-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="e18df-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="e18df-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="e18df-148">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="e18df-149">Configuring Microsoft Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="e18df-149">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="e18df-150">In this section, you enable Microsoft Azure AD SSO in the classic portal and configure single sign-on in your 8x8 Virtual Office application.</span><span class="sxs-lookup"><span data-stu-id="e18df-150">In this section, you enable Microsoft Azure AD SSO in the classic portal and configure single sign-on in your 8x8 Virtual Office application.</span></span>

<span data-ttu-id="e18df-151">**To configure Microsoft Azure AD Single Sign-On with 8x8 Virtual Office, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e18df-151">**To configure Microsoft Azure AD Single Sign-On with 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="e18df-152">In the classic portal, on the **8x8 Virtual Office** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="e18df-152">In the classic portal, on the **8x8 Virtual Office** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="e18df-154">On the **How would you like users to sign on to 8x8 Virtual Office** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e18df-154">On the **How would you like users to sign on to 8x8 Virtual Office** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_03.png) 
3. <span data-ttu-id="e18df-156">On the **Configure App Settings** dialog page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="e18df-156">On the **Configure App Settings** dialog page, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_04.png)
  1. <span data-ttu-id="e18df-158">In the **Reply URL** textbox, type: `https://sso.8x8.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="e18df-158">In the **Reply URL** textbox, type: `https://sso.8x8.com/saml2`</span></span>
  2. <span data-ttu-id="e18df-159">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e18df-159">Click **Next**.</span></span>
4. <span data-ttu-id="e18df-160">On the **Configure single sign-on at 8x8 Virtual Office** page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="e18df-160">On the **Configure single sign-on at 8x8 Virtual Office** page, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_05.png)
  1. <span data-ttu-id="e18df-162">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="e18df-162">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="e18df-163">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e18df-163">Click **Next**.</span></span>
5. <span data-ttu-id="e18df-164">Sign-on to your 8x8 Virtual Office tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="e18df-164">Sign-on to your 8x8 Virtual Office tenant as an administrator.</span></span>
6. <span data-ttu-id="e18df-165">Select **Virtual Office Account Mgr** on Application Panel.</span><span class="sxs-lookup"><span data-stu-id="e18df-165">Select **Virtual Office Account Mgr** on Application Panel.</span></span>
   
    ![Configure On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_001.png)
7. <span data-ttu-id="e18df-167">Select **Business** account to manage and click **Sign In** button.</span><span class="sxs-lookup"><span data-stu-id="e18df-167">Select **Business** account to manage and click **Sign In** button.</span></span>
   
    ![Configure On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_002.png)
8. <span data-ttu-id="e18df-169">Click **Accounts** tab in the menu list.</span><span class="sxs-lookup"><span data-stu-id="e18df-169">Click **Accounts** tab in the menu list.</span></span>
   
    ![Configure On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_003.png)
9. <span data-ttu-id="e18df-171">Click **Single Sign On** in the list of Accounts.</span><span class="sxs-lookup"><span data-stu-id="e18df-171">Click **Single Sign On** in the list of Accounts.</span></span>
   
    ![Configure On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_004.png)
10. <span data-ttu-id="e18df-173">Select **Signle Sign On** under Authentication method and click **SAML**.</span><span class="sxs-lookup"><span data-stu-id="e18df-173">Select **Signle Sign On** under Authentication method and click **SAML**.</span></span>
    
    ![Configure On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_005.png)
11. <span data-ttu-id="e18df-175">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD to **Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="e18df-175">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD to **Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span></span> 
    
    ![Configure On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_006.png)
    
    ![Configure On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_007.png)
12. <span data-ttu-id="e18df-178">Click **Browser** button to upload the certificate which you downloaded from Azure AD, and click the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="e18df-178">Click **Browser** button to upload the certificate which you downloaded from Azure AD, and click the **Save** button.</span></span>
13. <span data-ttu-id="e18df-179">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e18df-179">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD Single Sign-On][10]
14. <span data-ttu-id="e18df-181">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="e18df-181">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e18df-183">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e18df-183">Create an Azure AD test user</span></span>
<span data-ttu-id="e18df-184">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e18df-184">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="e18df-186">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e18df-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e18df-187">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e18df-187">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="e18df-189">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="e18df-189">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="e18df-190">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="e18df-190">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="e18df-192">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="e18df-192">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="e18df-194">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e18df-194">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="e18df-196">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="e18df-196">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="e18df-197">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e18df-197">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="e18df-198">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e18df-198">Click **Next**.</span></span>
6. <span data-ttu-id="e18df-199">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e18df-199">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="e18df-201">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="e18df-201">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="e18df-202">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="e18df-202">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="e18df-203">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e18df-203">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="e18df-204">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="e18df-204">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="e18df-205">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e18df-205">Click **Next**.</span></span>
7. <span data-ttu-id="e18df-206">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="e18df-206">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="e18df-208">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e18df-208">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="e18df-210">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="e18df-210">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="e18df-211">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="e18df-211">Click **Complete**.</span></span>   

### <a name="create-a-8x8-virtual-office-test-user"></a><span data-ttu-id="e18df-212">Create a 8x8 Virtual Office test user</span><span class="sxs-lookup"><span data-stu-id="e18df-212">Create a 8x8 Virtual Office test user</span></span>
<span data-ttu-id="e18df-213">The objective of this section is to create a user called Britta Simon in 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="e18df-213">The objective of this section is to create a user called Britta Simon in 8x8 Virtual Office.</span></span> <span data-ttu-id="e18df-214">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="e18df-214">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="e18df-215">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="e18df-215">There is no action item for you in this section.</span></span> <span data-ttu-id="e18df-216">A new user will be created during an attempt to access 8x8 Virtual Office if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="e18df-216">A new user will be created during an attempt to access 8x8 Virtual Office if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="e18df-217">If you need to create an user manually, you need to contact the 8x8 Virtual Office support team.</span><span class="sxs-lookup"><span data-stu-id="e18df-217">If you need to create an user manually, you need to contact the 8x8 Virtual Office support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e18df-218">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e18df-218">Assign the Azure AD test user</span></span>
<span data-ttu-id="e18df-219">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="e18df-219">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to 8x8 Virtual Office.</span></span>

![Assign User][200]

<span data-ttu-id="e18df-221">**To assign Britta Simon to 8x8 Virtual Office, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e18df-221">**To assign Britta Simon to 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="e18df-222">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="e18df-222">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201]
2. <span data-ttu-id="e18df-224">In the applications list, select **8x8 Virtual Office**.</span><span class="sxs-lookup"><span data-stu-id="e18df-224">In the applications list, select **8x8 Virtual Office**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_50.png)
3. <span data-ttu-id="e18df-226">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="e18df-226">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="e18df-228">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e18df-228">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="e18df-229">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="e18df-229">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="e18df-231">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="e18df-231">Test single sign-on</span></span>
<span data-ttu-id="e18df-232">The objective of this section is to test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="e18df-232">The objective of this section is to test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.</span></span>

<span data-ttu-id="e18df-233">When you click the 8x8 Virtual Office tile in the Access Panel, you should get automatically signed-on to your 8x8 Virtual Office application.</span><span class="sxs-lookup"><span data-stu-id="e18df-233">When you click the 8x8 Virtual Office tile in the Access Panel, you should get automatically signed-on to your 8x8 Virtual Office application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e18df-234">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e18df-234">Additional resources</span></span>
* [<span data-ttu-id="e18df-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e18df-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e18df-236">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e18df-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_205.png
































