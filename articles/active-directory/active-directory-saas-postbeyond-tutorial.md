---
title: 'Tutorial: Azure Active Directory integration with PostBeyond | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and PostBeyond.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 09992f08-ec50-4472-997f-ccbe719039e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: jeedes
ms.openlocfilehash: c6c06d108a68951b591fbdc1f9d9be7f56d35cf7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550453"
---
# <a name="tutorial-azure-active-directory-integration-with-postbeyond"></a><span data-ttu-id="e9aeb-103">Tutorial: Azure Active Directory integration with PostBeyond</span><span class="sxs-lookup"><span data-stu-id="e9aeb-103">Tutorial: Azure Active Directory integration with PostBeyond</span></span>
<span data-ttu-id="e9aeb-104">In this tutorial, you learn how to integrate PostBeyond with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e9aeb-104">In this tutorial, you learn how to integrate PostBeyond with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e9aeb-105">Integrating PostBeyond with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="e9aeb-105">Integrating PostBeyond with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="e9aeb-106">You can control in Azure AD who has access to PostBeyond</span><span class="sxs-lookup"><span data-stu-id="e9aeb-106">You can control in Azure AD who has access to PostBeyond</span></span>
* <span data-ttu-id="e9aeb-107">You can enable your users to automatically get signed-on to PostBeyond single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="e9aeb-107">You can enable your users to automatically get signed-on to PostBeyond single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="e9aeb-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="e9aeb-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="e9aeb-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e9aeb-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9aeb-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e9aeb-110">Prerequisites</span></span>
<span data-ttu-id="e9aeb-111">To configure Azure AD integration with PostBeyond, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="e9aeb-111">To configure Azure AD integration with PostBeyond, you need the following items:</span></span>

* <span data-ttu-id="e9aeb-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="e9aeb-112">An Azure AD subscription</span></span>
* <span data-ttu-id="e9aeb-113">A **PostBeyond** single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="e9aeb-113">A **PostBeyond** single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="e9aeb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="e9aeb-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="e9aeb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="e9aeb-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="e9aeb-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e9aeb-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e9aeb-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="e9aeb-118">Scenario description</span></span>
<span data-ttu-id="e9aeb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e9aeb-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="e9aeb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e9aeb-121">Adding PostBeyond from the gallery</span><span class="sxs-lookup"><span data-stu-id="e9aeb-121">Adding PostBeyond from the gallery</span></span>
2. <span data-ttu-id="e9aeb-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="e9aeb-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-postbeyond-from-the-gallery"></a><span data-ttu-id="e9aeb-123">Add PostBeyond from the gallery</span><span class="sxs-lookup"><span data-stu-id="e9aeb-123">Add PostBeyond from the gallery</span></span>
<span data-ttu-id="e9aeb-124">To configure the integration of PostBeyond into Azure AD, you need to add PostBeyond from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-124">To configure the integration of PostBeyond into Azure AD, you need to add PostBeyond from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e9aeb-125">**To add PostBeyond from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e9aeb-125">**To add PostBeyond from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e9aeb-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="e9aeb-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="e9aeb-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="e9aeb-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="e9aeb-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="e9aeb-135">In the search box, type **PostBeyond**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-135">In the search box, type **PostBeyond**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_01.png)
7. <span data-ttu-id="e9aeb-137">In the results pane, select **PostBeyond**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-137">In the results pane, select **PostBeyond**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="e9aeb-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="e9aeb-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="e9aeb-140">In this section, you configure and test Azure AD single sign-on with PostBeyond based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="e9aeb-140">In this section, you configure and test Azure AD single sign-on with PostBeyond based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e9aeb-141">For single sign-on to work, Azure AD needs to know what the counterpart user in PostBeyond is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-141">For single sign-on to work, Azure AD needs to know what the counterpart user in PostBeyond is to a user in Azure AD.</span></span> <span data-ttu-id="e9aeb-142">In other words, a link relationship between an Azure AD user and the related user in PostBeyond needs to be established.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-142">In other words, a link relationship between an Azure AD user and the related user in PostBeyond needs to be established.</span></span>

<span data-ttu-id="e9aeb-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in PostBeyond.</span></span>

<span data-ttu-id="e9aeb-144">To configure and test Azure AD single sign-on with PostBeyond, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e9aeb-144">To configure and test Azure AD single sign-on with PostBeyond, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e9aeb-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e9aeb-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e9aeb-147">**[Creating a PostBeyond test user](#creating-a-PostBeyond-test-user)** - to have a counterpart of Britta Simon in PostBeyond that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-147">**[Creating a PostBeyond test user](#creating-a-PostBeyond-test-user)** - to have a counterpart of Britta Simon in PostBeyond that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="e9aeb-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e9aeb-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="e9aeb-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="e9aeb-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="e9aeb-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your PostBeyond application.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your PostBeyond application.</span></span>

<span data-ttu-id="e9aeb-152">**To configure Azure AD SSO with PostBeyond, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e9aeb-152">**To configure Azure AD SSO with PostBeyond, perform the following steps:**</span></span>

1. <span data-ttu-id="e9aeb-153">In the menu on the top, click **Quick Start**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-153">In the menu on the top, click **Quick Start**.</span></span>
   
    ![Configure Single Sign-On][6]
2. <span data-ttu-id="e9aeb-155">In the classic portal, on the **PostBeyond** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-155">In the classic portal, on the **PostBeyond** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][7] 
3. <span data-ttu-id="e9aeb-157">On the **How would you like users to sign on to PostBeyond** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-157">On the **How would you like users to sign on to PostBeyond** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_06.png)
4. <span data-ttu-id="e9aeb-159">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e9aeb-159">On the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_07.png)
 1. <span data-ttu-id="e9aeb-161">In the Sign On URL text box, type a URL using the following pattern: `https://app.postbeyond.com`.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-161">In the Sign On URL text box, type a URL using the following pattern: `https://app.postbeyond.com`.</span></span> 
 2. <span data-ttu-id="e9aeb-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-162">Click **Next**.</span></span>

5. <span data-ttu-id="e9aeb-163">On the **Configure single sign-on at PostBeyond** page, Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-163">On the **Configure single sign-on at PostBeyond** page, Click **Download certificate**, and then save the file on your computer.</span></span> <span data-ttu-id="e9aeb-164">Also, copy the issuer URL, single sign-on service URL and single sign-out service URL values.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-164">Also, copy the issuer URL, single sign-on service URL and single sign-out service URL values.</span></span> <span data-ttu-id="e9aeb-165">You will need to share this information with PostBeyond support to get SSO configured.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-165">You will need to share this information with PostBeyond support to get SSO configured.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_08.png)
6. <span data-ttu-id="e9aeb-167">To get SSO configured for your application, contact PostBeyond support team at <mailto:sso@postbeyond.com>.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-167">To get SSO configured for your application, contact PostBeyond support team at <mailto:sso@postbeyond.com>.</span></span> <span data-ttu-id="e9aeb-168">They will assist with the proper channel to configure SSO and provide them the following:</span><span class="sxs-lookup"><span data-stu-id="e9aeb-168">They will assist with the proper channel to configure SSO and provide them the following:</span></span> 
   
   * <span data-ttu-id="e9aeb-169">The downloaded certificate</span><span class="sxs-lookup"><span data-stu-id="e9aeb-169">The downloaded certificate</span></span>
   * <span data-ttu-id="e9aeb-170">The **Issuer URL**</span><span class="sxs-lookup"><span data-stu-id="e9aeb-170">The **Issuer URL**</span></span>
   * <span data-ttu-id="e9aeb-171">The **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="e9aeb-171">The **SAML SSO URL**</span></span>
   * <span data-ttu-id="e9aeb-172">The **Single Sign-Out Service URL**</span><span class="sxs-lookup"><span data-stu-id="e9aeb-172">The **Single Sign-Out Service URL**</span></span>
7. <span data-ttu-id="e9aeb-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
8. <span data-ttu-id="e9aeb-175">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e9aeb-177">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e9aeb-177">Create an Azure AD test user</span></span>
<span data-ttu-id="e9aeb-178">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-178">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="e9aeb-180">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e9aeb-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e9aeb-181">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-181">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="e9aeb-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="e9aeb-184">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="e9aeb-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="e9aeb-188">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e9aeb-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/create_aaduser_05.png) 
 1. <span data-ttu-id="e9aeb-190">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-190">As Type Of User, select New user in your organization.</span></span> 
 2. <span data-ttu-id="e9aeb-191">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-191">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="e9aeb-192">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-192">Click **Next**.</span></span>
6. <span data-ttu-id="e9aeb-193">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e9aeb-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="e9aeb-195">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-195">In the **First Name** textbox, type **Britta**.</span></span>   
 2. <span data-ttu-id="e9aeb-196">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-196">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="e9aeb-197">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-197">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="e9aeb-198">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-198">In the **Role** list, select **User**.</span></span> 
 5. <span data-ttu-id="e9aeb-199">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-199">Click **Next**.</span></span>
7. <span data-ttu-id="e9aeb-200">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="e9aeb-202">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e9aeb-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="e9aeb-204">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-204">Write down the value of the **New Password**.</span></span> 
 2. <span data-ttu-id="e9aeb-205">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-205">Click **Complete**.</span></span>   

### <a name="create-a-postbeyond-test-user"></a><span data-ttu-id="e9aeb-206">Create a PostBeyond test user</span><span class="sxs-lookup"><span data-stu-id="e9aeb-206">Create a PostBeyond test user</span></span>
<span data-ttu-id="e9aeb-207">In this section, you create a user called Britta Simon in PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-207">In this section, you create a user called Britta Simon in PostBeyond.</span></span> <span data-ttu-id="e9aeb-208">If you don't know how to add Britta Simon in PostBeyond, please work with PostBeyond support team to add the test user and enable SSO.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-208">If you don't know how to add Britta Simon in PostBeyond, please work with PostBeyond support team to add the test user and enable SSO.</span></span> <span data-ttu-id="e9aeb-209">Contact them at <mailto:sso@postbeyond.com>.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-209">Contact them at <mailto:sso@postbeyond.com>.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e9aeb-210">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e9aeb-210">Assign the Azure AD test user</span></span>
<span data-ttu-id="e9aeb-211">In this section, you enable Britta Simon to use Azure SSO by granting her access to PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-211">In this section, you enable Britta Simon to use Azure SSO by granting her access to PostBeyond.</span></span>

![Assign User][200] 

<span data-ttu-id="e9aeb-213">**To assign Britta Simon to PostBeyond, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e9aeb-213">**To assign Britta Simon to PostBeyond, perform the following steps:**</span></span>

1. <span data-ttu-id="e9aeb-214">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-214">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="e9aeb-216">In the applications list, select **PostBeyond**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-216">In the applications list, select **PostBeyond**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_09.png) 
3. <span data-ttu-id="e9aeb-218">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-218">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="e9aeb-220">In the All Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-220">In the All Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="e9aeb-221">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-221">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="e9aeb-223">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="e9aeb-223">Test single sign-on</span></span>
<span data-ttu-id="e9aeb-224">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-224">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="e9aeb-225">When you click the PostBeyond tile in the Access Panel, you should get to the PostBeyond sign in page.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-225">When you click the PostBeyond tile in the Access Panel, you should get to the PostBeyond sign in page.</span></span> <span data-ttu-id="e9aeb-226">Click on **Sign in with Office 365**, enter your Azure AD credentials.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-226">Click on **Sign in with Office 365**, enter your Azure AD credentials.</span></span> <span data-ttu-id="e9aeb-227">Then, you should be logged in into PostBeyond.</span><span class="sxs-lookup"><span data-stu-id="e9aeb-227">Then, you should be logged in into PostBeyond.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e9aeb-228">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e9aeb-228">Additional resources</span></span>
* [<span data-ttu-id="e9aeb-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e9aeb-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e9aeb-230">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e9aeb-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/tutorial_general_04.png


[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/tutorial_general_05.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/tutorial_general_06.png
[7]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/tutorial_general_050.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/tutorial_general_060.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/tutorial_general_070.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-postbeyond-tutorial/tutorial_general_205.png



























