---
title: 'Tutorial: Azure Active Directory integration with TargetProcess | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and TargetProcess.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: d3ae285bf6399f14ca938268dec3672db8633ed8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550160"
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a><span data-ttu-id="c9085-103">Tutorial: Azure Active Directory integration with TargetProcess</span><span class="sxs-lookup"><span data-stu-id="c9085-103">Tutorial: Azure Active Directory integration with TargetProcess</span></span>
<span data-ttu-id="c9085-104">The objective of this tutorial is to show you how to integrate TargetProcess with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c9085-104">The objective of this tutorial is to show you how to integrate TargetProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c9085-105">Integrating TargetProcess with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="c9085-105">Integrating TargetProcess with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="c9085-106">You can control in Azure AD who has access to TargetProcess</span><span class="sxs-lookup"><span data-stu-id="c9085-106">You can control in Azure AD who has access to TargetProcess</span></span> 
* <span data-ttu-id="c9085-107">You can enable your users to automatically get signed-on to TargetProcess single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="c9085-107">You can enable your users to automatically get signed-on to TargetProcess single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="c9085-108">You can manage your accounts in one central location - the Azure Active Directory classic portal</span><span class="sxs-lookup"><span data-stu-id="c9085-108">You can manage your accounts in one central location - the Azure Active Directory classic portal</span></span>

<span data-ttu-id="c9085-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c9085-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9085-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c9085-110">Prerequisites</span></span>
<span data-ttu-id="c9085-111">To configure Azure AD integration with TargetProcess, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="c9085-111">To configure Azure AD integration with TargetProcess, you need the following items:</span></span>

* <span data-ttu-id="c9085-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="c9085-112">An Azure AD subscription</span></span>
* <span data-ttu-id="c9085-113">A TargetProcess SSO on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="c9085-113">A TargetProcess SSO on enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="c9085-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="c9085-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="c9085-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="c9085-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="c9085-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="c9085-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="c9085-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c9085-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="c9085-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="c9085-118">Scenario Description</span></span>
<span data-ttu-id="c9085-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="c9085-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="c9085-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="c9085-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c9085-121">Adding TargetProcess from the gallery</span><span class="sxs-lookup"><span data-stu-id="c9085-121">Adding TargetProcess from the gallery</span></span> 
2. <span data-ttu-id="c9085-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="c9085-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-targetprocess-from-the-gallery"></a><span data-ttu-id="c9085-123">Adding TargetProcess from the gallery</span><span class="sxs-lookup"><span data-stu-id="c9085-123">Adding TargetProcess from the gallery</span></span>
<span data-ttu-id="c9085-124">To configure the integration of TargetProcess into Azure AD, you need to add TargetProcess from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="c9085-124">To configure the integration of TargetProcess into Azure AD, you need to add TargetProcess from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c9085-125">**To add TargetProcess from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c9085-125">**To add TargetProcess from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c9085-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9085-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="c9085-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="c9085-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="c9085-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="c9085-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="c9085-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="c9085-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="c9085-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="c9085-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="c9085-135">In the search box, type **TargetProcess**.</span><span class="sxs-lookup"><span data-stu-id="c9085-135">In the search box, type **TargetProcess**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_target_process_01.png)
7. <span data-ttu-id="c9085-137">In the results pane, select **TargetProcess**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="c9085-137">In the results pane, select **TargetProcess**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_target_process_10.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="c9085-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="c9085-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="c9085-140">The objective of this section is to show you how to configure and test Azure AD SSO with TargetProcess based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c9085-140">The objective of this section is to show you how to configure and test Azure AD SSO with TargetProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c9085-141">For SSO to work, Azure AD needs to know what the counterpart user in TargetProcess to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="c9085-141">For SSO to work, Azure AD needs to know what the counterpart user in TargetProcess to an user in Azure AD is.</span></span> <span data-ttu-id="c9085-142">In other words, a link relationship between an Azure AD user and the related user in TargetProcess needs to be established.</span><span class="sxs-lookup"><span data-stu-id="c9085-142">In other words, a link relationship between an Azure AD user and the related user in TargetProcess needs to be established.</span></span>

<span data-ttu-id="c9085-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="c9085-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in TargetProcess.</span></span>

<span data-ttu-id="c9085-144">To configure and test Azure AD SSO with TargetProcess, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c9085-144">To configure and test Azure AD SSO with TargetProcess, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c9085-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="c9085-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c9085-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c9085-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c9085-147">**[Creating a TargetProcess test user](#creating-a-targetprocess-test-user)** - to have a counterpart of Britta Simon in TargetProcess that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="c9085-147">**[Creating a TargetProcess test user](#creating-a-targetprocess-test-user)** - to have a counterpart of Britta Simon in TargetProcess that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="c9085-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c9085-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c9085-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="c9085-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="c9085-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="c9085-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="c9085-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your TargetProcess application.</span><span class="sxs-lookup"><span data-stu-id="c9085-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your TargetProcess application.</span></span> 

<span data-ttu-id="c9085-152">As part of this procedure, you are required to create a base-64 encoded certificate file.</span><span class="sxs-lookup"><span data-stu-id="c9085-152">As part of this procedure, you are required to create a base-64 encoded certificate file.</span></span> <span data-ttu-id="c9085-153">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="c9085-153">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="c9085-154">To configure SSO for TargetProcess, you need a registered domain.</span><span class="sxs-lookup"><span data-stu-id="c9085-154">To configure SSO for TargetProcess, you need a registered domain.</span></span> <span data-ttu-id="c9085-155">If you don't have a registered domain yet, contact your TargetProcess support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span><span class="sxs-lookup"><span data-stu-id="c9085-155">If you don't have a registered domain yet, contact your TargetProcess support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span></span>  

<span data-ttu-id="c9085-156">**To configure Azure AD single sign-on with TargetProcess, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c9085-156">**To configure Azure AD single sign-on with TargetProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="c9085-157">In the Azure AD classic portal, on the **TargetProcess** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="c9085-157">In the Azure AD classic portal, on the **TargetProcess** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6]
2. <span data-ttu-id="c9085-159">On the **How would you like users to sign on to TargetProcess** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c9085-159">On the **How would you like users to sign on to TargetProcess** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_target_process_02.png) 
3. <span data-ttu-id="c9085-161">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c9085-161">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_target_process_03.png) 
  1. <span data-ttu-id="c9085-163">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your TargetProcess application (e.g.: *https://fabrikam.TargetProcess.com/*).</span><span class="sxs-lookup"><span data-stu-id="c9085-163">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your TargetProcess application (e.g.: *https://fabrikam.TargetProcess.com/*).</span></span>
  2. <span data-ttu-id="c9085-164">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c9085-164">Click **Next**.</span></span>
4. <span data-ttu-id="c9085-165">On the **Configure single sign-on at TargetProcess** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c9085-165">On the **Configure single sign-on at TargetProcess** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_target_process_04.png)   
  1. <span data-ttu-id="c9085-167">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="c9085-167">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="c9085-168">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c9085-168">Click **Next**.</span></span>
5. <span data-ttu-id="c9085-169">Sign-on to your TargetProcess application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="c9085-169">Sign-on to your TargetProcess application as an administrator.</span></span>
6. <span data-ttu-id="c9085-170">In the menu on the top, click **Setup**.</span><span class="sxs-lookup"><span data-stu-id="c9085-170">In the menu on the top, click **Setup**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)
7. <span data-ttu-id="c9085-172">Click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="c9085-172">Click **Settings**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 
8. <span data-ttu-id="c9085-174">Click **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c9085-174">Click **Single Sign-on**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 
9. <span data-ttu-id="c9085-176">On the Single Sign-on settings dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c9085-176">On the Single Sign-on settings dialog, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)   
  1. <span data-ttu-id="c9085-178">Click **Enable Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="c9085-178">Click **Enable Single Sign-on**.</span></span>
  2. <span data-ttu-id="c9085-179">In the Azure classic portal, on the **Configure single sign-on at TargetProcess** page, copy the **Single Sign-On Service URL** value, and then paste it into the **Sign-on URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="c9085-179">In the Azure classic portal, on the **Configure single sign-on at TargetProcess** page, copy the **Single Sign-On Service URL** value, and then paste it into the **Sign-on URL** textbox.</span></span>
  3. <span data-ttu-id="c9085-180">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="c9085-180">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span>
  4. <span data-ttu-id="c9085-181">click **Enable JIT Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="c9085-181">click **Enable JIT Provisioning**.</span></span>
10. <span data-ttu-id="c9085-182">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c9085-182">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Azure AD Single Sign-On][10]
11. <span data-ttu-id="c9085-184">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="c9085-184">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c9085-186">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c9085-186">Create an Azure AD test user</span></span>
<span data-ttu-id="c9085-187">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c9085-187">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

* <span data-ttu-id="c9085-188">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c9085-188">In the Users list, select **Britta Simon**.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="c9085-190">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c9085-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c9085-191">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9085-191">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/create_aaduser_09.png)  
2. <span data-ttu-id="c9085-193">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="c9085-193">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="c9085-194">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="c9085-194">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="c9085-196">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="c9085-196">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="c9085-198">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c9085-198">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/create_aaduser_05.png)   
  1. <span data-ttu-id="c9085-200">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="c9085-200">As Type Of User, select New user in your organization.</span></span> 
  2. <span data-ttu-id="c9085-201">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c9085-201">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="c9085-202">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c9085-202">Click **Next**.</span></span>
6. <span data-ttu-id="c9085-203">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c9085-203">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="c9085-205">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c9085-205">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="c9085-206">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c9085-206">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="c9085-207">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c9085-207">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="c9085-208">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="c9085-208">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="c9085-209">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c9085-209">Click **Next**.</span></span>
7. <span data-ttu-id="c9085-210">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="c9085-210">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="c9085-212">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c9085-212">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-flatter-files-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="c9085-214">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="c9085-214">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="c9085-215">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="c9085-215">Click **Complete**.</span></span>   

### <a name="create-a-targetprocess-test-user"></a><span data-ttu-id="c9085-216">Create a TargetProcess test user</span><span class="sxs-lookup"><span data-stu-id="c9085-216">Create a TargetProcess test user</span></span>
<span data-ttu-id="c9085-217">The objective of this section is to create a user called Britta Simon in TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="c9085-217">The objective of this section is to create a user called Britta Simon in TargetProcess.</span></span>

<span data-ttu-id="c9085-218">TargetProcess supports just-in-time provisioning.</span><span class="sxs-lookup"><span data-stu-id="c9085-218">TargetProcess supports just-in-time provisioning.</span></span> <span data-ttu-id="c9085-219">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="c9085-219">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

<span data-ttu-id="c9085-220">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="c9085-220">There is no action item for you in this section.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c9085-221">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c9085-221">Assign the Azure AD test user</span></span>
<span data-ttu-id="c9085-222">The objective of this section is to enabling Britta Simon to use Azure AD SSO by granting her access to TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="c9085-222">The objective of this section is to enabling Britta Simon to use Azure AD SSO by granting her access to TargetProcess.</span></span>

![Assign User][200] 

<span data-ttu-id="c9085-224">**To assign Britta Simon to TargetProcess, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c9085-224">**To assign Britta Simon to TargetProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="c9085-225">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="c9085-225">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="c9085-227">In the applications list, select **TargetProcess**.</span><span class="sxs-lookup"><span data-stu-id="c9085-227">In the applications list, select **TargetProcess**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_target_process_09.png) 
3. <span data-ttu-id="c9085-229">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="c9085-229">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="c9085-231">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c9085-231">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="c9085-232">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="c9085-232">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="c9085-234">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="c9085-234">Test single sign-on</span></span>
<span data-ttu-id="c9085-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c9085-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c9085-236">When you click the TargetProcess tile in the Access Panel, you should get automatically signed-on to your TargetProcess application.</span><span class="sxs-lookup"><span data-stu-id="c9085-236">When you click the TargetProcess tile in the Access Panel, you should get automatically signed-on to your TargetProcess application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c9085-237">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="c9085-237">Additional Resources</span></span>
* [<span data-ttu-id="c9085-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9085-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c9085-239">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c9085-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-target-process-tutorial/tutorial_general_205.png



































