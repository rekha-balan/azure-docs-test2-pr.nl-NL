---
title: 'Tutorial: Azure Active Directory integration with Origami | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Origami.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 48e1ac6431b44464691f0131d3489792cfd83587
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556681"
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a><span data-ttu-id="79946-103">Tutorial: Azure Active Directory integration with Origami</span><span class="sxs-lookup"><span data-stu-id="79946-103">Tutorial: Azure Active Directory integration with Origami</span></span>
<span data-ttu-id="79946-104">In this tutorial, you learn how to integrate Origami with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="79946-104">In this tutorial, you learn how to integrate Origami with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79946-105">Integrating Origami with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="79946-105">Integrating Origami with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="79946-106">You can control in Azure AD who has access to Origami</span><span class="sxs-lookup"><span data-stu-id="79946-106">You can control in Azure AD who has access to Origami</span></span>
* <span data-ttu-id="79946-107">You can enable your users to automatically get signed-on to Origami single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="79946-107">You can enable your users to automatically get signed-on to Origami single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="79946-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="79946-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="79946-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="79946-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79946-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="79946-110">Prerequisites</span></span>
<span data-ttu-id="79946-111">To configure Azure AD integration with Origami, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="79946-111">To configure Azure AD integration with Origami, you need the following items:</span></span>

* <span data-ttu-id="79946-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="79946-112">An Azure AD subscription</span></span>
* <span data-ttu-id="79946-113">A Origami single-sign (SSO) on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="79946-113">A Origami single-sign (SSO) on enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="79946-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="79946-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="79946-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="79946-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="79946-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="79946-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="79946-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="79946-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79946-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="79946-118">Scenario Description</span></span>
<span data-ttu-id="79946-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="79946-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="79946-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="79946-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79946-121">Adding Origami from the gallery</span><span class="sxs-lookup"><span data-stu-id="79946-121">Adding Origami from the gallery</span></span>
2. <span data-ttu-id="79946-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="79946-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-origami-from-the-gallery"></a><span data-ttu-id="79946-123">Add Origami from the gallery</span><span class="sxs-lookup"><span data-stu-id="79946-123">Add Origami from the gallery</span></span>
<span data-ttu-id="79946-124">To configure the integration of Origami into Azure AD, you need to add Origami from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="79946-124">To configure the integration of Origami into Azure AD, you need to add Origami from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="79946-125">**To add Origami from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="79946-125">**To add Origami from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="79946-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79946-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="79946-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="79946-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="79946-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="79946-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="79946-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="79946-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="79946-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="79946-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="79946-135">In the search box, type **Origami**.</span><span class="sxs-lookup"><span data-stu-id="79946-135">In the search box, type **Origami**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_origami_01.png)
7. <span data-ttu-id="79946-137">In the results pane, select **Origami**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="79946-137">In the results pane, select **Origami**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_origami_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="79946-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="79946-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="79946-140">In this section, you configure and test Azure AD SSO with Origami based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="79946-140">In this section, you configure and test Azure AD SSO with Origami based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="79946-141">For SSO to work, Azure AD needs to know what the counterpart user in Origami is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79946-141">For SSO to work, Azure AD needs to know what the counterpart user in Origami is to a user in Azure AD.</span></span> <span data-ttu-id="79946-142">In other words, a link relationship between an Azure AD user and the related user in Origami needs to be established.</span><span class="sxs-lookup"><span data-stu-id="79946-142">In other words, a link relationship between an Azure AD user and the related user in Origami needs to be established.</span></span>

<span data-ttu-id="79946-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Origami.</span><span class="sxs-lookup"><span data-stu-id="79946-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Origami.</span></span>

<span data-ttu-id="79946-144">To configure and test Azure AD SSO with Origami, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="79946-144">To configure and test Azure AD SSO with Origami, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="79946-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="79946-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="79946-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="79946-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79946-147">**[Creating a Origami test user](#creating-a-origami-test-user)** - to have a counterpart of Britta Simon in Origami that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="79946-147">**[Creating a Origami test user](#creating-a-origami-test-user)** - to have a counterpart of Britta Simon in Origami that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="79946-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="79946-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79946-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="79946-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="79946-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="79946-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="79946-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Origami application.</span><span class="sxs-lookup"><span data-stu-id="79946-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Origami application.</span></span>

<span data-ttu-id="79946-152">**To configure Azure AD single sign-on with Origami, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="79946-152">**To configure Azure AD single sign-on with Origami, perform the following steps:**</span></span>

1. <span data-ttu-id="79946-153">In the classic portal, on the **Origami** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="79946-153">In the classic portal, on the **Origami** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="79946-155">On the **How would you like users to sign on to Origami** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="79946-155">On the **How would you like users to sign on to Origami** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_origami_03.png) 
3. <span data-ttu-id="79946-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="79946-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_origami_04.png)
  1. <span data-ttu-id="79946-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Origami application using the following pattern: **https://live.origamirisk.com/origami/account/login?account=\<company name\>**</span><span class="sxs-lookup"><span data-stu-id="79946-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Origami application using the following pattern: **https://live.origamirisk.com/origami/account/login?account=\<company name\>**</span></span> 
  2. <span data-ttu-id="79946-160">click **Next**.</span><span class="sxs-lookup"><span data-stu-id="79946-160">click **Next**.</span></span>
4. <span data-ttu-id="79946-161">On the **Configure single sign-on at Origami** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="79946-161">On the **Configure single sign-on at Origami** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_origami_05.png)
  1. <span data-ttu-id="79946-163">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="79946-163">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="79946-164">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="79946-164">Click **Next**.</span></span>
5. <span data-ttu-id="79946-165">Log in to the Origami account with Admin rights.</span><span class="sxs-lookup"><span data-stu-id="79946-165">Log in to the Origami account with Admin rights.</span></span>
6. <span data-ttu-id="79946-166">In the menu on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="79946-166">In the menu on the top, click **Admin**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)
7. <span data-ttu-id="79946-168">On the Single Sign On Setup dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="79946-168">On the Single Sign On Setup dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/123.png)
  1. <span data-ttu-id="79946-170">Select **Enable Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="79946-170">Select **Enable Single Sign On**.</span></span>
  2. <span data-ttu-id="79946-171">In the Azure classic portal, copy the **SAML SSO URL**, and then paste it into the **Identity Provider's Sign-in Page URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="79946-171">In the Azure classic portal, copy the **SAML SSO URL**, and then paste it into the **Identity Provider's Sign-in Page URL** textbox.</span></span>
  3. <span data-ttu-id="79946-172">In the Azure classic portal, copy the **SINGLE SIGN OUT SERVICE URL**, and then paste it into the **Identity Provider's Sign-out Page URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="79946-172">In the Azure classic portal, copy the **SINGLE SIGN OUT SERVICE URL**, and then paste it into the **Identity Provider's Sign-out Page URL** textbox.</span></span>
  4. <span data-ttu-id="79946-173">Click **Browse** to upload the certificate you have downloaded from the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="79946-173">Click **Browse** to upload the certificate you have downloaded from the Azure classic portal.</span></span>
  5. <span data-ttu-id="79946-174">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="79946-174">Click **Save Changes**.</span></span>
8. <span data-ttu-id="79946-175">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="79946-175">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
9. <span data-ttu-id="79946-177">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="79946-177">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="79946-179">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="79946-179">Create an Azure AD test user</span></span>
<span data-ttu-id="79946-180">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="79946-180">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="79946-182">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="79946-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="79946-183">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79946-183">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="79946-185">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="79946-185">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="79946-186">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="79946-186">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="79946-188">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="79946-188">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="79946-190">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/create_aaduser_05.png)</span><span class="sxs-lookup"><span data-stu-id="79946-190">On the **Tell us about this user** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/create_aaduser_05.png)</span></span> 
  1. <span data-ttu-id="79946-191">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="79946-191">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="79946-192">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="79946-192">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="79946-193">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="79946-193">Click **Next**.</span></span>
6. <span data-ttu-id="79946-194">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="79946-194">On the **User Profile** dialog page, perform the following steps:</span></span>

  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="79946-196">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="79946-196">In the **First Name** textbox, type **Britta**.</span></span>    
  2. <span data-ttu-id="79946-197">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="79946-197">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="79946-198">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="79946-198">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="79946-199">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="79946-199">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="79946-200">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="79946-200">Click **Next**.</span></span>
7. <span data-ttu-id="79946-201">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="79946-201">On the **Get temporary password** dialog page, click **create**.</span></span>
   
  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="79946-203">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="79946-203">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/create_aaduser_08.png)  
  1. <span data-ttu-id="79946-205">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="79946-205">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="79946-206">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="79946-206">Click **Complete**.</span></span>   

### <a name="create-an-origami-test-user"></a><span data-ttu-id="79946-207">Create an Origami test user</span><span class="sxs-lookup"><span data-stu-id="79946-207">Create an Origami test user</span></span>
<span data-ttu-id="79946-208">In this section, you create a user called Britta Simon in Origami.</span><span class="sxs-lookup"><span data-stu-id="79946-208">In this section, you create a user called Britta Simon in Origami.</span></span> 

1. <span data-ttu-id="79946-209">Log in to the Origami account with Admin rights.</span><span class="sxs-lookup"><span data-stu-id="79946-209">Log in to the Origami account with Admin rights.</span></span>
2. <span data-ttu-id="79946-210">In the menu on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="79946-210">In the menu on the top, click **Admin**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)
3. <span data-ttu-id="79946-212">On the **Users and Security** dialog, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="79946-212">On the **Users and Security** dialog, click **Users**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)
4. <span data-ttu-id="79946-214">Click **Add New User**.</span><span class="sxs-lookup"><span data-stu-id="79946-214">Click **Add New User**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)
5. <span data-ttu-id="79946-216">On the Add New User dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="79946-216">On the Add New User dialog, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)
  1. <span data-ttu-id="79946-218">In the **User Name** textbox, type User Name of Britta Simon in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="79946-218">In the **User Name** textbox, type User Name of Britta Simon in the Azure classic portal.</span></span>
  2. <span data-ttu-id="79946-219">In the **Password** textbox, type a passwotd.</span><span class="sxs-lookup"><span data-stu-id="79946-219">In the **Password** textbox, type a passwotd.</span></span>
  3. <span data-ttu-id="79946-220">In the **Confirm Password** textbox, type the password again.</span><span class="sxs-lookup"><span data-stu-id="79946-220">In the **Confirm Password** textbox, type the password again.</span></span>
  4. <span data-ttu-id="79946-221">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="79946-221">In the **First Name** textbox, type **Britta**.</span></span>
  5. <span data-ttu-id="79946-222">In the **Last Name** textbox, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="79946-222">In the **Last Name** textbox, type **Simon**.</span></span>
  6. <span data-ttu-id="79946-223">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="79946-223">Click **Save**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)
6. <span data-ttu-id="79946-225">Assign **User Roles** and **Client Access** to the user.</span><span class="sxs-lookup"><span data-stu-id="79946-225">Assign **User Roles** and **Client Access** to the user.</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="79946-227">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="79946-227">Assign the Azure AD test user</span></span>
<span data-ttu-id="79946-228">In this section, you enable Britta Simon to use Azure SSO by granting her access to Origami.</span><span class="sxs-lookup"><span data-stu-id="79946-228">In this section, you enable Britta Simon to use Azure SSO by granting her access to Origami.</span></span>

![Assign User][200] 

<span data-ttu-id="79946-230">**To assign Britta Simon to Origami, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="79946-230">**To assign Britta Simon to Origami, perform the following steps:**</span></span>

1. <span data-ttu-id="79946-231">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="79946-231">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="79946-233">In the applications list, select **Origami**.</span><span class="sxs-lookup"><span data-stu-id="79946-233">In the applications list, select **Origami**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_origami_50.png) 
3. <span data-ttu-id="79946-235">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="79946-235">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="79946-237">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="79946-237">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="79946-238">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="79946-238">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="79946-240">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="79946-240">Test single sign-on</span></span>
<span data-ttu-id="79946-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="79946-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="79946-242">When you click the Origami tile in the Access Panel, you should get automatically signed-on to your Origami application.</span><span class="sxs-lookup"><span data-stu-id="79946-242">When you click the Origami tile in the Access Panel, you should get automatically signed-on to your Origami application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="79946-243">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="79946-243">Additional Resources</span></span>
* [<span data-ttu-id="79946-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79946-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79946-245">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="79946-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-origami-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-origami-tutorial/tutorial_general_205.png

































