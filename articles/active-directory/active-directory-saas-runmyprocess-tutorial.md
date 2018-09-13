---
title: 'Tutorial: Azure Active Directory integration with RunMyProcess | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and RunMyProcess.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: jeedes
ms.openlocfilehash: 4fe2e6a8ce9135d756fc0602bd3d50552a25ed11
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551634"
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a><span data-ttu-id="c60c9-103">Tutorial: Azure Active Directory integration with RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="c60c9-103">Tutorial: Azure Active Directory integration with RunMyProcess</span></span>
<span data-ttu-id="c60c9-104">The objective of this tutorial is to show you how to integrate RunMyProcess with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c60c9-104">The objective of this tutorial is to show you how to integrate RunMyProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c60c9-105">Integrating RunMyProcess with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="c60c9-105">Integrating RunMyProcess with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="c60c9-106">You can control in Azure AD who has access to RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="c60c9-106">You can control in Azure AD who has access to RunMyProcess</span></span>
* <span data-ttu-id="c60c9-107">You can enable your users to automatically get signed-on to RunMyProcess single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="c60c9-107">You can enable your users to automatically get signed-on to RunMyProcess single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="c60c9-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="c60c9-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="c60c9-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c60c9-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c60c9-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c60c9-110">Prerequisites</span></span>
<span data-ttu-id="c60c9-111">To configure Azure AD integration with RunMyProcess, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="c60c9-111">To configure Azure AD integration with RunMyProcess, you need the following items:</span></span>

* <span data-ttu-id="c60c9-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="c60c9-112">An Azure AD subscription</span></span>
* <span data-ttu-id="c60c9-113">A RunMyProcess SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="c60c9-113">A RunMyProcess SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="c60c9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="c60c9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="c60c9-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="c60c9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="c60c9-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="c60c9-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="c60c9-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c60c9-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c60c9-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="c60c9-118">Scenario description</span></span>
<span data-ttu-id="c60c9-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="c60c9-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="c60c9-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="c60c9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c60c9-121">Adding RunMyProcess from the gallery</span><span class="sxs-lookup"><span data-stu-id="c60c9-121">Adding RunMyProcess from the gallery</span></span>
2. <span data-ttu-id="c60c9-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="c60c9-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-runmyprocess-from-the-gallery"></a><span data-ttu-id="c60c9-123">Add RunMyProcess from the gallery</span><span class="sxs-lookup"><span data-stu-id="c60c9-123">Add RunMyProcess from the gallery</span></span>
<span data-ttu-id="c60c9-124">To configure the integration of RunMyProcess into Azure AD, you need to add RunMyProcess from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="c60c9-124">To configure the integration of RunMyProcess into Azure AD, you need to add RunMyProcess from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c60c9-125">**To add RunMyProcess from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c60c9-125">**To add RunMyProcess from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c60c9-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="c60c9-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="c60c9-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="c60c9-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="c60c9-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="c60c9-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="c60c9-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="c60c9-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="c60c9-135">In the search box, type **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-135">In the search box, type **RunMyProcess**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_01.png)
7. <span data-ttu-id="c60c9-137">In the results pane, select **RunMyProcess**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="c60c9-137">In the results pane, select **RunMyProcess**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_0001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="c60c9-139">Configure and test Azure AD SSo</span><span class="sxs-lookup"><span data-stu-id="c60c9-139">Configure and test Azure AD SSo</span></span>
<span data-ttu-id="c60c9-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="c60c9-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c60c9-141">For single sign-on to work, Azure AD needs to know what the counterpart user in RunMyProcess is to a user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="c60c9-141">For single sign-on to work, Azure AD needs to know what the counterpart user in RunMyProcess is to a user in Azure AD is.</span></span> <span data-ttu-id="c60c9-142">In other words, a link relationship between an Azure AD user and the related user in RunMyProcess needs to be established.</span><span class="sxs-lookup"><span data-stu-id="c60c9-142">In other words, a link relationship between an Azure AD user and the related user in RunMyProcess needs to be established.</span></span>

<span data-ttu-id="c60c9-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="c60c9-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in RunMyProcess.</span></span>

<span data-ttu-id="c60c9-144">To configure and test Azure AD SSO with RunMyProcess, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="c60c9-144">To configure and test Azure AD SSO with RunMyProcess, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c60c9-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="c60c9-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c60c9-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c60c9-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c60c9-147">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - to have a counterpart of Britta Simon in RunMyProcess that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="c60c9-147">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - to have a counterpart of Britta Simon in RunMyProcess that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="c60c9-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="c60c9-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c60c9-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="c60c9-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="c60c9-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="c60c9-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="c60c9-151">In this section, you enable Azure AD single sign-on in the classic portal and configure SSO in your RunMyProcess application.</span><span class="sxs-lookup"><span data-stu-id="c60c9-151">In this section, you enable Azure AD single sign-on in the classic portal and configure SSO in your RunMyProcess application.</span></span>

<span data-ttu-id="c60c9-152">**To configure Azure AD SSO with RunMyProcess, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c60c9-152">**To configure Azure AD SSO with RunMyProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="c60c9-153">In the classic portal, on the **RunMyProcess** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="c60c9-153">In the classic portal, on the **RunMyProcess** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="c60c9-155">On the **How would you like users to sign on to RunMyProcess** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-155">On the **How would you like users to sign on to RunMyProcess** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_03.png) 
3. <span data-ttu-id="c60c9-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c60c9-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_04.png) 
  1. <span data-ttu-id="c60c9-159">In the **Sign On URL** textbox, type a URL using the following pattern: `https://live.runmyprocess.com/live/<tenant id>`.</span><span class="sxs-lookup"><span data-stu-id="c60c9-159">In the **Sign On URL** textbox, type a URL using the following pattern: `https://live.runmyprocess.com/live/<tenant id>`.</span></span> 
  2. <span data-ttu-id="c60c9-160">click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-160">click **Next**.</span></span>
    >[!NOTE]
    ><span data-ttu-id="c60c9-161">Please note that you have to update the value with the actual Sign On URL.</span><span class="sxs-lookup"><span data-stu-id="c60c9-161">Please note that you have to update the value with the actual Sign On URL.</span></span> <span data-ttu-id="c60c9-162">To get this value, contact RunMyProcess support team via <mailto:support@runmyprocess.com>.</span><span class="sxs-lookup"><span data-stu-id="c60c9-162">To get this value, contact RunMyProcess support team via <mailto:support@runmyprocess.com>.</span></span>
    >  
4. <span data-ttu-id="c60c9-163">On the **Configure single sign-on at RunMyProcess** page, click **Download Certificate** and then save the file on your computer:</span><span class="sxs-lookup"><span data-stu-id="c60c9-163">On the **Configure single sign-on at RunMyProcess** page, click **Download Certificate** and then save the file on your computer:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_05.png)
5. <span data-ttu-id="c60c9-165">In a different web browser window, sign-on to your RunMyProcess tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="c60c9-165">In a different web browser window, sign-on to your RunMyProcess tenant as an administrator.</span></span>
6. <span data-ttu-id="c60c9-166">In left navigation panel, click **Account** and select **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-166">In left navigation panel, click **Account** and select **Configuration**.</span></span>
   
    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)
7. <span data-ttu-id="c60c9-168">Go to **Authentication method** section and perform below steps:</span><span class="sxs-lookup"><span data-stu-id="c60c9-168">Go to **Authentication method** section and perform below steps:</span></span>
   
    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)
  1. <span data-ttu-id="c60c9-170">As **Method**, select **SSO with Samlv2**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-170">As **Method**, select **SSO with Samlv2**.</span></span> 
  2. <span data-ttu-id="c60c9-171">In the **SSO redirect** textbox put the value of **SAML SSO URL** from Azure AD application configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="c60c9-171">In the **SSO redirect** textbox put the value of **SAML SSO URL** from Azure AD application configuration wizard.</span></span>
  3. <span data-ttu-id="c60c9-172">In the **Logout redirect** textbox put the value of **Single Sign-Out Service URL** from Azure AD application configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="c60c9-172">In the **Logout redirect** textbox put the value of **Single Sign-Out Service URL** from Azure AD application configuration wizard.</span></span>
  4. <span data-ttu-id="c60c9-173">In the **Name Id Format** textbox put the value of **Name Identifier Format** from Azure AD application configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="c60c9-173">In the **Name Id Format** textbox put the value of **Name Identifier Format** from Azure AD application configuration wizard.</span></span>
  5. <span data-ttu-id="c60c9-174">Copy the content of the downloaded certificate file and then paste it into the **Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="c60c9-174">Copy the content of the downloaded certificate file and then paste it into the **Certificate** textbox.</span></span> 
  6. <span data-ttu-id="c60c9-175">Click **Save** icon.</span><span class="sxs-lookup"><span data-stu-id="c60c9-175">Click **Save** icon.</span></span>
8. <span data-ttu-id="c60c9-176">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-176">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
9. <span data-ttu-id="c60c9-178">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-178">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c60c9-180">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c60c9-180">Create an Azure AD test user</span></span>
<span data-ttu-id="c60c9-181">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c60c9-181">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="c60c9-183">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c60c9-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c60c9-184">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-184">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 
2. <span data-ttu-id="c60c9-186">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="c60c9-186">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="c60c9-187">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-187">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 
4. <span data-ttu-id="c60c9-189">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-189">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 
5. <span data-ttu-id="c60c9-191">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c60c9-191">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 
 1. <span data-ttu-id="c60c9-193">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="c60c9-193">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="c60c9-194">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-194">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="c60c9-195">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-195">Click **Next**.</span></span>
6. <span data-ttu-id="c60c9-196">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c60c9-196">On the **User Profile** dialog page, perform the following steps:</span></span>

   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="c60c9-198">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-198">In the **First Name** textbox, type **Britta**.</span></span>   
 2. <span data-ttu-id="c60c9-199">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-199">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="c60c9-200">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-200">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="c60c9-201">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-201">In the **Role** list, select **User**.</span></span> 
 5. <span data-ttu-id="c60c9-202">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-202">Click **Next**.</span></span>
7. <span data-ttu-id="c60c9-203">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-203">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/create_aaduser_06.png) 
8. <span data-ttu-id="c60c9-205">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c60c9-205">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/create_aaduser_07.png)  
 1. <span data-ttu-id="c60c9-207">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-207">Write down the value of the **New Password**.</span></span>
 2. <span data-ttu-id="c60c9-208">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-208">Click **Complete**.</span></span>   

### <a name="create-a-runmyprocess-test-user"></a><span data-ttu-id="c60c9-209">Create a RunMyProcess test user</span><span class="sxs-lookup"><span data-stu-id="c60c9-209">Create a RunMyProcess test user</span></span>
<span data-ttu-id="c60c9-210">In order to enable Azure AD users to log into RunMyProcess, they must be provisioned into RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="c60c9-210">In order to enable Azure AD users to log into RunMyProcess, they must be provisioned into RunMyProcess.</span></span> <span data-ttu-id="c60c9-211">In the case of RunMyProcess, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="c60c9-211">In the case of RunMyProcess, provisioning is a manual task.</span></span>

<span data-ttu-id="c60c9-212">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c60c9-212">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="c60c9-213">Log in to your RunMyProcess company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="c60c9-213">Log in to your RunMyProcess company site as an administrator.</span></span>
2. <span data-ttu-id="c60c9-214">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-214">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span></span>
   
   <span data-ttu-id="c60c9-215">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span><span class="sxs-lookup"><span data-stu-id="c60c9-215">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span></span>
3. <span data-ttu-id="c60c9-216">In the **User Settings** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="c60c9-216">In the **User Settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="c60c9-217">![Profile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span><span class="sxs-lookup"><span data-stu-id="c60c9-217">![Profile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span></span>   
 1. <span data-ttu-id="c60c9-218">Type the **Name** and **E-mail** of a valid AAD account you want to provision into the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="c60c9-218">Type the **Name** and **E-mail** of a valid AAD account you want to provision into the related textboxes.</span></span> 
 2. <span data-ttu-id="c60c9-219">Select an **IDE language**, a **Language** and a **Profile**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-219">Select an **IDE language**, a **Language** and a **Profile**.</span></span> 
 3. <span data-ttu-id="c60c9-220">Select **Send account creation e-mail to me**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-220">Select **Send account creation e-mail to me**.</span></span> 
 4. <span data-ttu-id="c60c9-221">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-221">Click **Save**.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="c60c9-222">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess to provision Azure Active Directory user accounts.</span><span class="sxs-lookup"><span data-stu-id="c60c9-222">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess to provision Azure Active Directory user accounts.</span></span> 
   > 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c60c9-223">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="c60c9-223">Assign the Azure AD test user</span></span>
<span data-ttu-id="c60c9-224">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to RunMyProcess.</span><span class="sxs-lookup"><span data-stu-id="c60c9-224">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to RunMyProcess.</span></span>

![Assign User][200] 

<span data-ttu-id="c60c9-226">**To assign Britta Simon to RunMyProcess, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="c60c9-226">**To assign Britta Simon to RunMyProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="c60c9-227">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="c60c9-227">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="c60c9-229">In the applications list, select **RunMyProcess**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-229">In the applications list, select **RunMyProcess**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_50.png) 
3. <span data-ttu-id="c60c9-231">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-231">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="c60c9-233">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-233">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="c60c9-234">bar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="c60c9-234">bar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="c60c9-236">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="c60c9-236">Test single sign-on</span></span>
<span data-ttu-id="c60c9-237">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="c60c9-237">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="c60c9-238">When you click the RunMyProcess tile in the Access Panel, you should get automatically signed-on to your RunMyProcess application.</span><span class="sxs-lookup"><span data-stu-id="c60c9-238">When you click the RunMyProcess tile in the Access Panel, you should get automatically signed-on to your RunMyProcess application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c60c9-239">Additional resources</span><span class="sxs-lookup"><span data-stu-id="c60c9-239">Additional resources</span></span>
* [<span data-ttu-id="c60c9-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c60c9-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c60c9-241">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c60c9-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-runmyprocess-tutorial/tutorial_general_205.png





























