---
title: 'Tutorial: Azure Active Directory integration with Recognize | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Recognize.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: jeedes
ms.openlocfilehash: 5a8e6b9dddface892b6d6af3d6b3cf8b29cb2340
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660522"
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a><span data-ttu-id="b0cfb-103">Tutorial: Azure Active Directory integration with Recognize</span><span class="sxs-lookup"><span data-stu-id="b0cfb-103">Tutorial: Azure Active Directory integration with Recognize</span></span>
<span data-ttu-id="b0cfb-104">The objective of this tutorial is to show you how to integrate Recognize with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b0cfb-104">The objective of this tutorial is to show you how to integrate Recognize with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b0cfb-105">Integrating Recognize with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="b0cfb-105">Integrating Recognize with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="b0cfb-106">You can control in Azure AD who has access to Recognize</span><span class="sxs-lookup"><span data-stu-id="b0cfb-106">You can control in Azure AD who has access to Recognize</span></span>
* <span data-ttu-id="b0cfb-107">You can enable your users to automatically get signed-on to Recognize single sign-on) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="b0cfb-107">You can enable your users to automatically get signed-on to Recognize single sign-on) with their Azure AD accounts</span></span>
* <span data-ttu-id="b0cfb-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="b0cfb-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="b0cfb-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b0cfb-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0cfb-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b0cfb-110">Prerequisites</span></span>
<span data-ttu-id="b0cfb-111">To configure Azure AD integration with Recognize, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="b0cfb-111">To configure Azure AD integration with Recognize, you need the following items:</span></span>

* <span data-ttu-id="b0cfb-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="b0cfb-112">An Azure AD subscription</span></span>
* <span data-ttu-id="b0cfb-113">A Recognize single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="b0cfb-113">A Recognize single-sign on (SSO) enabled subscription</span></span>

 >[!NOTE]
 ><span data-ttu-id="b0cfb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
 > 

<span data-ttu-id="b0cfb-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="b0cfb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="b0cfb-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="b0cfb-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b0cfb-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b0cfb-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="b0cfb-118">Scenario description</span></span>
<span data-ttu-id="b0cfb-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="b0cfb-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="b0cfb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b0cfb-121">Adding Recognize from the gallery</span><span class="sxs-lookup"><span data-stu-id="b0cfb-121">Adding Recognize from the gallery</span></span>
2. <span data-ttu-id="b0cfb-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="b0cfb-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-recognize-from-the-gallery"></a><span data-ttu-id="b0cfb-123">Adding Recognize from the gallery</span><span class="sxs-lookup"><span data-stu-id="b0cfb-123">Adding Recognize from the gallery</span></span>
<span data-ttu-id="b0cfb-124">To configure the integration of Recognize into Azure AD, you need to add Recognize from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-124">To configure the integration of Recognize into Azure AD, you need to add Recognize from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b0cfb-125">**To add Recognize from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b0cfb-125">**To add Recognize from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b0cfb-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="b0cfb-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="b0cfb-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="b0cfb-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="b0cfb-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="b0cfb-135">In the search box, type **Recognize**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-135">In the search box, type **Recognize**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_recognize_01.png)
7. <span data-ttu-id="b0cfb-137">In the results panel, select **Recognize**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-137">In the results panel, select **Recognize**, and then click **Complete** to add the application.</span></span>
   
    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_recognize_0001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="b0cfb-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="b0cfb-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="b0cfb-140">The objective of this section is to show you how to configure and test Azure AD SSO with Recognize based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b0cfb-140">The objective of this section is to show you how to configure and test Azure AD SSO with Recognize based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b0cfb-141">For SSO to work, Azure AD needs to know what the counterpart user in Recognize to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-141">For SSO to work, Azure AD needs to know what the counterpart user in Recognize to an user in Azure AD is.</span></span> <span data-ttu-id="b0cfb-142">In other words, a link relationship between an Azure AD user and the related user in Recognize needs to be established.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-142">In other words, a link relationship between an Azure AD user and the related user in Recognize needs to be established.</span></span>

<span data-ttu-id="b0cfb-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Recognize.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Recognize.</span></span>

<span data-ttu-id="b0cfb-144">To configure and test Azure AD SSO with Recognize, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b0cfb-144">To configure and test Azure AD SSO with Recognize, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b0cfb-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b0cfb-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b0cfb-147">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - to have a counterpart of Britta Simon in Recognize that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-147">**[Creating a Recognize test user](#creating-a-recognize-test-user)** - to have a counterpart of Britta Simon in Recognize that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="b0cfb-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b0cfb-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="b0cfb-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="b0cfb-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="b0cfb-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Recognize application.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Recognize application.</span></span>

<span data-ttu-id="b0cfb-152">**To configure Azure AD SSO with Recognize, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b0cfb-152">**To configure Azure AD SSO with Recognize, perform the following steps:**</span></span>

1. <span data-ttu-id="b0cfb-153">In the classic portal, on the **Recognize** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-153">In the classic portal, on the **Recognize** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="b0cfb-155">On the **How would you like users to sign on to Recognize** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-155">On the **How would you like users to sign on to Recognize** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_recognize_03.png)
3. <span data-ttu-id="b0cfb-157">On the **Configure App Settings** dialog page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="b0cfb-157">On the **Configure App Settings** dialog page, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_recognize_04.png)
  1. <span data-ttu-id="b0cfb-159">In the **Sign On URL** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-159">In the **Sign On URL** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>/saml/sso`.</span></span> 
  2. <span data-ttu-id="b0cfb-160">In the **Identifier** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>/saml/metadata`.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-160">In the **Identifier** textbox, type a URL using the following pattern: `https://recognizeapp.com/<your-domain>/saml/metadata`.</span></span>
  3. <span data-ttu-id="b0cfb-161">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-161">Click **Next**.</span></span>
  
    >[!NOTE]
    ><span data-ttu-id="b0cfb-162">If you don't know about these URLs, type sample URLs with example pattern.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-162">If you don't know about these URLs, type sample URLs with example pattern.</span></span> <span data-ttu-id="b0cfb-163">To get these values, you can refer step 9 for more details or contact Recognize support team via <mailto:support@recognizeapp.com>.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-163">To get these values, you can refer step 9 for more details or contact Recognize support team via <mailto:support@recognizeapp.com>.</span></span>
    >

4. <span data-ttu-id="b0cfb-164">On the **Configure single sign-on at Recognize** page, click **Download certificate** and then save the file on your computer:</span><span class="sxs-lookup"><span data-stu-id="b0cfb-164">On the **Configure single sign-on at Recognize** page, click **Download certificate** and then save the file on your computer:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_recognize_05.png)
5. <span data-ttu-id="b0cfb-166">In a different web browser window, sign-on to your Recognize tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-166">In a different web browser window, sign-on to your Recognize tenant as an administrator.</span></span>
6. <span data-ttu-id="b0cfb-167">On the upper right corner, click **Menu**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-167">On the upper right corner, click **Menu**.</span></span> <span data-ttu-id="b0cfb-168">Go to **Company Admin**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-168">Go to **Company Admin**.</span></span>
   
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)
7. <span data-ttu-id="b0cfb-170">On the left navigation pane, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-170">On the left navigation pane, click **Settings**.</span></span>
   
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)
8. <span data-ttu-id="b0cfb-172">Perform the following steps on **SSO Settings** section.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-172">Perform the following steps on **SSO Settings** section.</span></span>
   
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
 1. <span data-ttu-id="b0cfb-174">As **Enable SSO**, select **ON**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-174">As **Enable SSO**, select **ON**.</span></span>
 2. <span data-ttu-id="b0cfb-175">In the **IDP Entity ID** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-175">In the **IDP Entity ID** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span></span> 
 3. <span data-ttu-id="b0cfb-176">In the **Sso target url** textbox put the value of **Single Sign-On Service URL** from Azure AD application configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-176">In the **Sso target url** textbox put the value of **Single Sign-On Service URL** from Azure AD application configuration wizard.</span></span> 
 4. <span data-ttu-id="b0cfb-177">In the **Slo target url** textbox put the value of **Single Sign-Out Service URL** from Azure AD application configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-177">In the **Slo target url** textbox put the value of **Single Sign-Out Service URL** from Azure AD application configuration wizard.</span></span> 
 5. <span data-ttu-id="b0cfb-178">Open your downloaded certificate file in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-178">Open your downloaded certificate file in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox.</span></span>  
 6. <span data-ttu-id="b0cfb-179">Click the **Save settings** button.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-179">Click the **Save settings** button.</span></span> 
9. <span data-ttu-id="b0cfb-180">Beside the **SSO Settings** section, copy the URL under **Service Provider Metadata url**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-180">Beside the **SSO Settings** section, copy the URL under **Service Provider Metadata url**.</span></span>
   
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)
10. <span data-ttu-id="b0cfb-182">Open the **Metadata URL link** under a blank browser to download the metadata document.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-182">Open the **Metadata URL link** under a blank browser to download the metadata document.</span></span> <span data-ttu-id="b0cfb-183">Then use the EntityDescriptor value Recognize provided you for **Identifier** on the **Configure App Settings** dialog.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-183">Then use the EntityDescriptor value Recognize provided you for **Identifier** on the **Configure App Settings** dialog.</span></span>
    
    ![Configure Single Sign-On On App side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)
11. <span data-ttu-id="b0cfb-185">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-185">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD Single Sign-On][10]
12. <span data-ttu-id="b0cfb-187">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-187">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b0cfb-189">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b0cfb-189">Create an Azure AD test user</span></span>
<span data-ttu-id="b0cfb-190">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-190">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="b0cfb-192">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b0cfb-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b0cfb-193">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-193">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="b0cfb-195">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-195">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="b0cfb-196">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-196">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="b0cfb-198">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-198">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="b0cfb-200">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b0cfb-200">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/create_aaduser_05.png)
 1. <span data-ttu-id="b0cfb-202">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-202">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="b0cfb-203">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-203">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="b0cfb-204">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-204">Click **Next**.</span></span>
6. <span data-ttu-id="b0cfb-205">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b0cfb-205">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/create_aaduser_06.png) 
 1. <span data-ttu-id="b0cfb-207">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-207">In the **First Name** textbox, type **Britta**.</span></span>   
 2. <span data-ttu-id="b0cfb-208">In the **Last Name** textbox, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-208">In the **Last Name** textbox, type **Simon**.</span></span> 
 3. <span data-ttu-id="b0cfb-209">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-209">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="b0cfb-210">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-210">In the **Role** list, select **User**.</span></span> 
 5. <span data-ttu-id="b0cfb-211">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-211">Click **Next**.</span></span>
7. <span data-ttu-id="b0cfb-212">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-212">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="b0cfb-214">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b0cfb-214">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/create_aaduser_08.png) 
 1. <span data-ttu-id="b0cfb-216">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-216">Write down the value of the **New Password**.</span></span> 
 2. <span data-ttu-id="b0cfb-217">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-217">Click **Complete**.</span></span>   

### <a name="create-a-recognize-test-user"></a><span data-ttu-id="b0cfb-218">Create a Recognize test user</span><span class="sxs-lookup"><span data-stu-id="b0cfb-218">Create a Recognize test user</span></span>
<span data-ttu-id="b0cfb-219">In order to enable Azure AD users to log into Recognize, they must be provisioned into Recognize.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-219">In order to enable Azure AD users to log into Recognize, they must be provisioned into Recognize.</span></span> <span data-ttu-id="b0cfb-220">In the case of Recognize, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-220">In the case of Recognize, provisioning is a manual task.</span></span>

<span data-ttu-id="b0cfb-221">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-221">This app doesn't support SCIM provisioning but has an alternate user sync that provisions users.</span></span> 

<span data-ttu-id="b0cfb-222">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b0cfb-222">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="b0cfb-223">Log into your Recognize company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-223">Log into your Recognize company site as an administrator.</span></span>
2. <span data-ttu-id="b0cfb-224">On the upper right corner, click **Menu**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-224">On the upper right corner, click **Menu**.</span></span> <span data-ttu-id="b0cfb-225">Go to **Company Admin**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-225">Go to **Company Admin**.</span></span>
3. <span data-ttu-id="b0cfb-226">On the left navigation pane, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-226">On the left navigation pane, click **Settings**.</span></span>
4. <span data-ttu-id="b0cfb-227">Perform the following steps on **User Sync** section.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-227">Perform the following steps on **User Sync** section.</span></span>
   
   <span data-ttu-id="b0cfb-228">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "New User")</span><span class="sxs-lookup"><span data-stu-id="b0cfb-228">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "New User")</span></span>   
 1. <span data-ttu-id="b0cfb-229">As **Sync Enabled**, select **ON**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-229">As **Sync Enabled**, select **ON**.</span></span> 
 2. <span data-ttu-id="b0cfb-230">As **Choose sync provider**, select **Microsoft / Office 365**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-230">As **Choose sync provider**, select **Microsoft / Office 365**.</span></span> 
 3. <span data-ttu-id="b0cfb-231">Click **Run User Sync**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-231">Click **Run User Sync**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b0cfb-232">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b0cfb-232">Assign the Azure AD test user</span></span>
<span data-ttu-id="b0cfb-233">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Recognize.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-233">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Recognize.</span></span>

![Assign User][200]

<span data-ttu-id="b0cfb-235">**To assign Britta Simon to Recognize, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b0cfb-235">**To assign Britta Simon to Recognize, perform the following steps:**</span></span>

1. <span data-ttu-id="b0cfb-236">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-236">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201]
2. <span data-ttu-id="b0cfb-238">In the applications list, select **Recognize**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-238">In the applications list, select **Recognize**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_recognize_50.png)
3. <span data-ttu-id="b0cfb-240">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-240">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="b0cfb-242">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-242">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="b0cfb-243">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-243">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="b0cfb-245">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="b0cfb-245">Test single sign-on</span></span>
<span data-ttu-id="b0cfb-246">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-246">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="b0cfb-247">When you click the Recognize tile in the Access Panel, you should get automatically signed-on to your Recognize application.</span><span class="sxs-lookup"><span data-stu-id="b0cfb-247">When you click the Recognize tile in the Access Panel, you should get automatically signed-on to your Recognize application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b0cfb-248">Additional resources</span><span class="sxs-lookup"><span data-stu-id="b0cfb-248">Additional resources</span></span>
* [<span data-ttu-id="b0cfb-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0cfb-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b0cfb-250">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b0cfb-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-recognize-tutorial/tutorial_general_205.png































