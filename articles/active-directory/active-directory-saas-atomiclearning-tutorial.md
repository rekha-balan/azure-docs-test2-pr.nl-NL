---
title: 'Tutorial: Azure Active Directory integration with Atomic Learning | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Atomic Learning.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 495f54a6-e6c4-41b0-aafa-a6283d33efc8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f7d12f02bc4496460085a276bcfa9f081bc4a4bf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555705"
---
# <a name="tutorial-azure-active-directory-integration-with-atomic-learning"></a><span data-ttu-id="7e4b3-103">Tutorial: Azure Active Directory integration with Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="7e4b3-103">Tutorial: Azure Active Directory integration with Atomic Learning</span></span>
<span data-ttu-id="7e4b3-104">In this tutorial, you learn how to integrate Atomic Learning with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7e4b3-104">In this tutorial, you learn how to integrate Atomic Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7e4b3-105">Integrating Atomic Learning with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="7e4b3-105">Integrating Atomic Learning with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="7e4b3-106">You can control in Azure AD who has access to Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="7e4b3-106">You can control in Azure AD who has access to Atomic Learning</span></span>
* <span data-ttu-id="7e4b3-107">You can enable your users to automatically get signed-on to Atomic Learning (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="7e4b3-107">You can enable your users to automatically get signed-on to Atomic Learning (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="7e4b3-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="7e4b3-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="7e4b3-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7e4b3-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e4b3-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7e4b3-110">Prerequisites</span></span>
<span data-ttu-id="7e4b3-111">To configure Azure AD integration with Atomic Learning, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="7e4b3-111">To configure Azure AD integration with Atomic Learning, you need the following items:</span></span>

* <span data-ttu-id="7e4b3-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="7e4b3-112">An Azure AD subscription</span></span>
* <span data-ttu-id="7e4b3-113">A **Atomic Learning** single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="7e4b3-113">A **Atomic Learning** single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7e4b3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="7e4b3-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="7e4b3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="7e4b3-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="7e4b3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e4b3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7e4b3-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="7e4b3-118">Scenario description</span></span>
<span data-ttu-id="7e4b3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7e4b3-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="7e4b3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7e4b3-121">Adding Atomic Learning from the gallery</span><span class="sxs-lookup"><span data-stu-id="7e4b3-121">Adding Atomic Learning from the gallery</span></span>
2. <span data-ttu-id="7e4b3-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7e4b3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atomic-learning-from-the-gallery"></a><span data-ttu-id="7e4b3-123">Adding Atomic Learning from the gallery</span><span class="sxs-lookup"><span data-stu-id="7e4b3-123">Adding Atomic Learning from the gallery</span></span>
<span data-ttu-id="7e4b3-124">To configure the integration of Atomic Learning into Azure AD, you need to add Atomic Learning from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-124">To configure the integration of Atomic Learning into Azure AD, you need to add Atomic Learning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7e4b3-125">**To add Atomic Learning from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7e4b3-125">**To add Atomic Learning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7e4b3-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="7e4b3-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="7e4b3-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="7e4b3-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="7e4b3-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="7e4b3-135">In the search box, type **Atomic Learning**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-135">In the search box, type **Atomic Learning**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_01.png)

7. <span data-ttu-id="7e4b3-137">In the results pane, select **Atomic Learning**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-137">In the results pane, select **Atomic Learning**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7e4b3-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7e4b3-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7e4b3-140">In this section, you configure and test Azure AD single sign-on with Atomic Learning based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="7e4b3-140">In this section, you configure and test Azure AD single sign-on with Atomic Learning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7e4b3-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Atomic Learning is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Atomic Learning is to a user in Azure AD.</span></span> <span data-ttu-id="7e4b3-142">In other words, a link relationship between an Azure AD user and the related user in Atomic Learning needs to be established.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-142">In other words, a link relationship between an Azure AD user and the related user in Atomic Learning needs to be established.</span></span>
<span data-ttu-id="7e4b3-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Atomic Learning.</span></span>

<span data-ttu-id="7e4b3-144">To configure and test Azure AD single sign-on with Atomic Learning, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="7e4b3-144">To configure and test Azure AD single sign-on with Atomic Learning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7e4b3-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7e4b3-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7e4b3-147">**[Creating an Atomic Learning test user](#creating-an-atomic-learning-test-user)** - to have a counterpart of Britta Simon in Atomic Learning that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-147">**[Creating an Atomic Learning test user](#creating-an-atomic-learning-test-user)** - to have a counterpart of Britta Simon in Atomic Learning that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="7e4b3-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7e4b3-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7e4b3-150">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="7e4b3-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="7e4b3-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Atomic Learning application.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Atomic Learning application.</span></span>

<span data-ttu-id="7e4b3-152">**To configure Azure AD single sign-on with Atomic Learning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7e4b3-152">**To configure Azure AD single sign-on with Atomic Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="7e4b3-153">In the menu on the top, click **Quick Start**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-153">In the menu on the top, click **Quick Start**.</span></span>
   
    ![Configure Single Sign-On][6]

2. <span data-ttu-id="7e4b3-155">In the classic portal, on the **Atomic Learning** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-155">In the classic portal, on the **Atomic Learning** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][7] 

3. <span data-ttu-id="7e4b3-157">On the **How would you like users to sign on to Atomic Learning** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-157">On the **How would you like users to sign on to Atomic Learning** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_06.png)

4. <span data-ttu-id="7e4b3-159">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e4b3-159">On the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_07.png)

    <span data-ttu-id="7e4b3-161">a.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-161">a.</span></span> <span data-ttu-id="7e4b3-162">In the Sign On URL text box, type a URL using the following pattern: `https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-162">In the Sign On URL text box, type a URL using the following pattern: `https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`.</span></span>

    <span data-ttu-id="7e4b3-163">b.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-163">b.</span></span> <span data-ttu-id="7e4b3-164">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-164">Click **Next**.</span></span>

1. <span data-ttu-id="7e4b3-165">On the **Configure single sign-on at Atomic Learning** page, Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-165">On the **Configure single sign-on at Atomic Learning** page, Click **Download metadata**, and then save the file on your computer.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_08.png)

2. <span data-ttu-id="7e4b3-167">To get SSO configured for your application, contact Atomic Learning support.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-167">To get SSO configured for your application, contact Atomic Learning support.</span></span> <span data-ttu-id="7e4b3-168">They will assist with the proper channel to configure SSO.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-168">They will assist with the proper channel to configure SSO.</span></span> <span data-ttu-id="7e4b3-169">Please note that you have to send email and attach downloaded metadata file to <mailto:cs@atomiclearning.com></span><span class="sxs-lookup"><span data-stu-id="7e4b3-169">Please note that you have to send email and attach downloaded metadata file to <mailto:cs@atomiclearning.com></span></span>

3. <span data-ttu-id="7e4b3-170">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-170">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]

4. <span data-ttu-id="7e4b3-172">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-172">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7e4b3-174">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7e4b3-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="7e4b3-175">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-175">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="7e4b3-177">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7e4b3-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7e4b3-178">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-178">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="7e4b3-180">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-180">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="7e4b3-181">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-181">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7e4b3-183">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-183">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="7e4b3-185">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e4b3-185">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="7e4b3-187">a.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-187">a.</span></span> <span data-ttu-id="7e4b3-188">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-188">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="7e4b3-189">b.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-189">b.</span></span> <span data-ttu-id="7e4b3-190">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-190">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="7e4b3-191">c.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-191">c.</span></span> <span data-ttu-id="7e4b3-192">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-192">Click **Next**.</span></span>

6. <span data-ttu-id="7e4b3-193">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e4b3-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="7e4b3-195">a.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-195">a.</span></span> <span data-ttu-id="7e4b3-196">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-196">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="7e4b3-197">b.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-197">b.</span></span> <span data-ttu-id="7e4b3-198">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-198">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="7e4b3-199">c.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-199">c.</span></span> <span data-ttu-id="7e4b3-200">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-200">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="7e4b3-201">d.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-201">d.</span></span> <span data-ttu-id="7e4b3-202">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-202">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="7e4b3-203">e.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-203">e.</span></span> <span data-ttu-id="7e4b3-204">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-204">Click **Next**.</span></span>

7. <span data-ttu-id="7e4b3-205">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-205">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="7e4b3-207">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="7e4b3-207">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="7e4b3-209">a.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-209">a.</span></span> <span data-ttu-id="7e4b3-210">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-210">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="7e4b3-211">b.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-211">b.</span></span> <span data-ttu-id="7e4b3-212">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-212">Click **Complete**.</span></span>   

### <a name="creating-a-atomic-learning-test-user"></a><span data-ttu-id="7e4b3-213">Creating a Atomic Learning test user</span><span class="sxs-lookup"><span data-stu-id="7e4b3-213">Creating a Atomic Learning test user</span></span>
<span data-ttu-id="7e4b3-214">In this section, you create a user called Britta Simon in Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-214">In this section, you create a user called Britta Simon in Atomic Learning.</span></span> <span data-ttu-id="7e4b3-215">Atomic Learning supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-215">Atomic Learning supports just-in-time provisioning, which is by default enabled.</span></span> 

<span data-ttu-id="7e4b3-216">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-216">There is no action item for you in this section.</span></span> <span data-ttu-id="7e4b3-217">A new user will be created during an attempt to access Atomic Learning if it doesn't exist yet using the email address for the user.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-217">A new user will be created during an attempt to access Atomic Learning if it doesn't exist yet using the email address for the user.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7e4b3-218">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="7e4b3-218">Assigning the Azure AD test user</span></span>
<span data-ttu-id="7e4b3-219">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-219">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Atomic Learning.</span></span>

![Assign User][200] 

<span data-ttu-id="7e4b3-221">**To assign Britta Simon to Atomic Learning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7e4b3-221">**To assign Britta Simon to Atomic Learning, perform the following steps:**</span></span>

1. <span data-ttu-id="7e4b3-222">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-222">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="7e4b3-224">In the applications list, select **Atomic Learning**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-224">In the applications list, select **Atomic Learning**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_09.png) 
3. <span data-ttu-id="7e4b3-226">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-226">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="7e4b3-228">In the All Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-228">In the All Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="7e4b3-229">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-229">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="7e4b3-231">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="7e4b3-231">Testing single sign-on</span></span>
<span data-ttu-id="7e4b3-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-232">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7e4b3-233">When you click the Atomic Learning tile in the Access Panel, you should get automatically signed-on to your Atomic Learning application.</span><span class="sxs-lookup"><span data-stu-id="7e4b3-233">When you click the Atomic Learning tile in the Access Panel, you should get automatically signed-on to your Atomic Learning application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7e4b3-234">Additional resources</span><span class="sxs-lookup"><span data-stu-id="7e4b3-234">Additional resources</span></span>
* [<span data-ttu-id="7e4b3-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e4b3-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7e4b3-236">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7e4b3-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/tutorial_general_04.png


[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/tutorial_general_05.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/tutorial_general_06.png
[7]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/tutorial_general_050.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/tutorial_general_060.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/tutorial_general_070.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-atomiclearning-tutorial/tutorial_general_205.png



























