---
title: 'Tutorial: Azure Active Directory integration with Kiteworks | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Kiteworks.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: f7984aaf-ab1f-4a85-9646-a9523f5275d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: jeedes
ms.openlocfilehash: ab42548374bd101cb0262d7974e7bf897caa0fa0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553866"
---
# <a name="tutorial-azure-active-directory-integration-with-kiteworks"></a><span data-ttu-id="d6a51-103">Tutorial: Azure Active Directory integration with Kiteworks</span><span class="sxs-lookup"><span data-stu-id="d6a51-103">Tutorial: Azure Active Directory integration with Kiteworks</span></span>
<span data-ttu-id="d6a51-104">The objective of this tutorial is to show you how to integrate Kiteworks with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d6a51-104">The objective of this tutorial is to show you how to integrate Kiteworks with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="d6a51-105">Integrating Kiteworks with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d6a51-105">Integrating Kiteworks with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="d6a51-106">You can control in Azure AD who has access to Kiteworks</span><span class="sxs-lookup"><span data-stu-id="d6a51-106">You can control in Azure AD who has access to Kiteworks</span></span> 
* <span data-ttu-id="d6a51-107">You can enable your users to automatically get signed-on to Kiteworks aingle aign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="d6a51-107">You can enable your users to automatically get signed-on to Kiteworks aingle aign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="d6a51-108">You can manage your accounts in one central location - the Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6a51-108">You can manage your accounts in one central location - the Azure Active Directory</span></span> 

<span data-ttu-id="d6a51-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d6a51-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6a51-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d6a51-110">Prerequisites</span></span>
<span data-ttu-id="d6a51-111">To configure Azure AD integration with Kiteworks, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d6a51-111">To configure Azure AD integration with Kiteworks, you need the following items:</span></span>

* <span data-ttu-id="d6a51-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d6a51-112">An Azure AD subscription</span></span>
* <span data-ttu-id="d6a51-113">A Kiteworks SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d6a51-113">A Kiteworks SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="d6a51-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d6a51-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="d6a51-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d6a51-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="d6a51-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="d6a51-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="d6a51-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d6a51-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="d6a51-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="d6a51-118">Scenario Description</span></span>
<span data-ttu-id="d6a51-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d6a51-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>  

<span data-ttu-id="d6a51-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d6a51-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d6a51-121">Adding Kiteworks from the gallery</span><span class="sxs-lookup"><span data-stu-id="d6a51-121">Adding Kiteworks from the gallery</span></span> 
2. <span data-ttu-id="d6a51-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="d6a51-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-kiteworks-from-the-gallery"></a><span data-ttu-id="d6a51-123">Add Kiteworks from the gallery</span><span class="sxs-lookup"><span data-stu-id="d6a51-123">Add Kiteworks from the gallery</span></span>
<span data-ttu-id="d6a51-124">To configure the integration of Kiteworks into Azure AD, you need to add Kiteworks from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d6a51-124">To configure the integration of Kiteworks into Azure AD, you need to add Kiteworks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d6a51-125">**To add Kiteworks from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d6a51-125">**To add Kiteworks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d6a51-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="d6a51-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="d6a51-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d6a51-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="d6a51-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="d6a51-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="d6a51-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="d6a51-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="d6a51-135">In the search box, type **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-135">In the search box, type **Kiteworks**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_01.png)
7. <span data-ttu-id="d6a51-137">In the results pane, select **Kiteworks**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="d6a51-137">In the results pane, select **Kiteworks**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_02.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d6a51-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d6a51-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="d6a51-140">The objective of this section is to show you how to configure and test Azure AD SSO with Kiteworks based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d6a51-140">The objective of this section is to show you how to configure and test Azure AD SSO with Kiteworks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d6a51-141">For SSO to work, Azure AD needs to know what the counterpart user in Kiteworks to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="d6a51-141">For SSO to work, Azure AD needs to know what the counterpart user in Kiteworks to an user in Azure AD is.</span></span> <span data-ttu-id="d6a51-142">In other words, a link relationship between an Azure AD user and the related user in Kiteworks needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d6a51-142">In other words, a link relationship between an Azure AD user and the related user in Kiteworks needs to be established.</span></span>

<span data-ttu-id="d6a51-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="d6a51-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Kiteworks.</span></span>

<span data-ttu-id="d6a51-144">To configure and test Azure AD SSO with Kiteworks, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d6a51-144">To configure and test Azure AD SSO with Kiteworks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d6a51-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d6a51-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d6a51-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d6a51-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d6a51-147">**[Creating a Kiteworks test user](#creating-a-kiteworks-test-user)** - to have a counterpart of Britta Simon in Kiteworks that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="d6a51-147">**[Creating a Kiteworks test user](#creating-a-kiteworks-test-user)** - to have a counterpart of Britta Simon in Kiteworks that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="d6a51-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d6a51-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d6a51-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d6a51-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="d6a51-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="d6a51-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="d6a51-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Kiteworks application.</span><span class="sxs-lookup"><span data-stu-id="d6a51-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Kiteworks application.</span></span> 

<span data-ttu-id="d6a51-152">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="d6a51-152">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span> <span data-ttu-id="d6a51-153">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="d6a51-153">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="d6a51-154">To configure SSO for Kiteworks, you need a registered domain.</span><span class="sxs-lookup"><span data-stu-id="d6a51-154">To configure SSO for Kiteworks, you need a registered domain.</span></span> <span data-ttu-id="d6a51-155">If you don't have a registered domain yet, contact your Kiteworks support team.</span><span class="sxs-lookup"><span data-stu-id="d6a51-155">If you don't have a registered domain yet, contact your Kiteworks support team.</span></span>  

<span data-ttu-id="d6a51-156">**To configure Azure AD single sign-on with Kiteworks, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d6a51-156">**To configure Azure AD single sign-on with Kiteworks, perform the following steps:**</span></span>

1. <span data-ttu-id="d6a51-157">In the Azure classic portal, on the **Kiteworks** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="d6a51-157">In the Azure classic portal, on the **Kiteworks** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="d6a51-159">On the **How would you like users to sign on to Kiteworks** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-159">On the **How would you like users to sign on to Kiteworks** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_03.png) 
3. <span data-ttu-id="d6a51-161">On the **Configure App Settings** dialog page, perform the following steps:.</span><span class="sxs-lookup"><span data-stu-id="d6a51-161">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_04.png) 
  1. <span data-ttu-id="d6a51-163">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Kiteworks application (e.g.: *https://fabrikam.kiteworks.com/*).</span><span class="sxs-lookup"><span data-stu-id="d6a51-163">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Kiteworks application (e.g.: *https://fabrikam.kiteworks.com/*).</span></span>
  2. <span data-ttu-id="d6a51-164">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-164">Click **Next**.</span></span>
4. <span data-ttu-id="d6a51-165">On the **Configure single sign-on at Kiteworks** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d6a51-165">On the **Configure single sign-on at Kiteworks** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_05.png)   
  1. <span data-ttu-id="d6a51-167">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d6a51-167">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="d6a51-168">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-168">Click **Next**.</span></span>
5. <span data-ttu-id="d6a51-169">Sign on to your Kiteworks company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="d6a51-169">Sign on to your Kiteworks company site as an administrator.</span></span>
6. <span data-ttu-id="d6a51-170">In the toolbar on the top, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-170">In the toolbar on the top, click **Settings**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_06.png) 
7. <span data-ttu-id="d6a51-172">In the **Authentication and Authorization** section, click **SSO Setup**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-172">In the **Authentication and Authorization** section, click **SSO Setup**.</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_07.png) 
8. <span data-ttu-id="d6a51-174">On the SSO Setup page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d6a51-174">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_09.png)   
  1. <span data-ttu-id="d6a51-176">Select **Authenticate via SSO**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-176">Select **Authenticate via SSO**.</span></span>
  2. <span data-ttu-id="d6a51-177">Select **Initiate AuthnRequest**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-177">Select **Initiate AuthnRequest**.</span></span>
  3. <span data-ttu-id="d6a51-178">In the Azure classic portal, on the **Configure single sign-on at Kiteworks** dialog page, copy the **Entity ID** value, and then paste it into the **IDP Entity ID** textbox.</span><span class="sxs-lookup"><span data-stu-id="d6a51-178">In the Azure classic portal, on the **Configure single sign-on at Kiteworks** dialog page, copy the **Entity ID** value, and then paste it into the **IDP Entity ID** textbox.</span></span> 
  4. <span data-ttu-id="d6a51-179">In the Azure classic portal, on the **Configure single sign-on at Kiteworks** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **Single Sign-On Service URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="d6a51-179">In the Azure classic portal, on the **Configure single sign-on at Kiteworks** dialog page, copy the **Single Sign-On Service URL** value, and then paste it into the **Single Sign-On Service URL** textbox.</span></span>
  5. <span data-ttu-id="d6a51-180">In the Azure classic portal, on the **Configure single sign-on at Kiteworks** dialog page, copy the **Single Sign-Out Service URL** value, and then paste it into the **Single Logout Service URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="d6a51-180">In the Azure classic portal, on the **Configure single sign-on at Kiteworks** dialog page, copy the **Single Sign-Out Service URL** value, and then paste it into the **Single Logout Service URL** textbox.</span></span>
  6. <span data-ttu-id="d6a51-181">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **RSA Public Key Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="d6a51-181">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **RSA Public Key Certificate** textbox.</span></span> 
  7. <span data-ttu-id="d6a51-182">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-182">Click **Save**.</span></span>
9. <span data-ttu-id="d6a51-183">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-183">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Azure AD Single Sign-On][10]
10. <span data-ttu-id="d6a51-185">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-185">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d6a51-187">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d6a51-187">Create an Azure AD test user</span></span>
<span data-ttu-id="d6a51-188">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d6a51-188">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="d6a51-190">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d6a51-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d6a51-191">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-191">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/create_aaduser_09.png)  
2. <span data-ttu-id="d6a51-193">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="d6a51-193">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="d6a51-194">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-194">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="d6a51-196">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-196">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="d6a51-198">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d6a51-198">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/create_aaduser_05.png)  
  1. <span data-ttu-id="d6a51-200">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="d6a51-200">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="d6a51-201">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-201">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="d6a51-202">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-202">Click **Next**.</span></span>
6. <span data-ttu-id="d6a51-203">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d6a51-203">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="d6a51-205">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-205">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="d6a51-206">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-206">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="d6a51-207">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-207">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="d6a51-208">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-208">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="d6a51-209">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-209">Click **Next**.</span></span>
7. <span data-ttu-id="d6a51-210">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-210">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="d6a51-212">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d6a51-212">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="d6a51-214">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-214">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="d6a51-215">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-215">Click **Complete**.</span></span>   

### <a name="create-a-kiteworks-test-user"></a><span data-ttu-id="d6a51-216">Create a Kiteworks test user</span><span class="sxs-lookup"><span data-stu-id="d6a51-216">Create a Kiteworks test user</span></span>
<span data-ttu-id="d6a51-217">The objective of this section is to create a user called Britta Simon in Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="d6a51-217">The objective of this section is to create a user called Britta Simon in Kiteworks.</span></span>

<span data-ttu-id="d6a51-218">Kiteworks supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="d6a51-218">Kiteworks supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="d6a51-219">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="d6a51-219">There is no action item for you in this section.</span></span> <span data-ttu-id="d6a51-220">A new user will be created during an attempt to access Kitewors if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="d6a51-220">A new user will be created during an attempt to access Kitewors if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="d6a51-221">If you need to create an user manually, you need to contact the Kiteworks support team.</span><span class="sxs-lookup"><span data-stu-id="d6a51-221">If you need to create an user manually, you need to contact the Kiteworks support team.</span></span>
>  

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d6a51-222">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d6a51-222">Assign the Azure AD test user</span></span>
<span data-ttu-id="d6a51-223">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="d6a51-223">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Kiteworks.</span></span>

![Assign User][200] 

<span data-ttu-id="d6a51-225">**To assign Britta Simon to Kiteworks, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d6a51-225">**To assign Britta Simon to Kiteworks, perform the following steps:**</span></span>

1. <span data-ttu-id="d6a51-226">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="d6a51-226">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="d6a51-228">In the applications list, select **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-228">In the applications list, select **Kiteworks**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_50.png) 
3. <span data-ttu-id="d6a51-230">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-230">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="d6a51-232">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-232">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="d6a51-233">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="d6a51-233">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="d6a51-235">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="d6a51-235">Test single sign-on</span></span>
<span data-ttu-id="d6a51-236">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d6a51-236">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="d6a51-237">When you click the Kiteworks tile in the Access Panel, you should get automatically signed-on to your Kiteworks application.</span><span class="sxs-lookup"><span data-stu-id="d6a51-237">When you click the Kiteworks tile in the Access Panel, you should get automatically signed-on to your Kiteworks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d6a51-238">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="d6a51-238">Additional Resources</span></span>
* [<span data-ttu-id="d6a51-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6a51-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d6a51-240">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d6a51-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-kiteworks-tutorial/tutorial_general_205.png


































