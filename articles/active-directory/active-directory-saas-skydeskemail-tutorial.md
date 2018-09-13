---
title: 'Tutorial: Azure Active Directory integration with SkyDesk Email | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and SkyDesk Email.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: d7c12a75b7921f9eb90831ca523b9ab6786b1e4d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563162"
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a><span data-ttu-id="b4173-103">Tutorial: Azure Active Directory integration with SkyDesk Email</span><span class="sxs-lookup"><span data-stu-id="b4173-103">Tutorial: Azure Active Directory integration with SkyDesk Email</span></span>
<span data-ttu-id="b4173-104">The objective of this tutorial is to show you how to integrate SkyDesk Email with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b4173-104">The objective of this tutorial is to show you how to integrate SkyDesk Email with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b4173-105">Integrating SkyDesk Email with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="b4173-105">Integrating SkyDesk Email with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="b4173-106">You can control in Azure AD who has access to SkyDesk Email</span><span class="sxs-lookup"><span data-stu-id="b4173-106">You can control in Azure AD who has access to SkyDesk Email</span></span>
* <span data-ttu-id="b4173-107">You can enable your users to automatically get signed-on to SkyDesk Email single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="b4173-107">You can enable your users to automatically get signed-on to SkyDesk Email single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="b4173-108">You can manage your accounts in one central location - the Azure Active Directory classic portal</span><span class="sxs-lookup"><span data-stu-id="b4173-108">You can manage your accounts in one central location - the Azure Active Directory classic portal</span></span>

<span data-ttu-id="b4173-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b4173-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4173-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b4173-110">Prerequisites</span></span>
<span data-ttu-id="b4173-111">To configure Azure AD integration with SkyDesk Email, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="b4173-111">To configure Azure AD integration with SkyDesk Email, you need the following items:</span></span>

* <span data-ttu-id="b4173-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="b4173-112">An Azure AD subscription</span></span>
* <span data-ttu-id="b4173-113">A SkyDesk Email single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="b4173-113">A SkyDesk Email single sign-on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="b4173-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="b4173-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="b4173-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="b4173-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="b4173-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="b4173-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="b4173-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b4173-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b4173-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="b4173-118">Scenario Description</span></span>
<span data-ttu-id="b4173-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="b4173-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="b4173-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="b4173-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b4173-121">Adding SkyDesk Email from the gallery</span><span class="sxs-lookup"><span data-stu-id="b4173-121">Adding SkyDesk Email from the gallery</span></span>
2. <span data-ttu-id="b4173-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="b4173-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-skydesk-email-from-the-gallery"></a><span data-ttu-id="b4173-123">Add SkyDesk Email from the gallery</span><span class="sxs-lookup"><span data-stu-id="b4173-123">Add SkyDesk Email from the gallery</span></span>
<span data-ttu-id="b4173-124">To configure the integration of SkyDesk Email into Azure AD, you need to add SkyDesk Email from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="b4173-124">To configure the integration of SkyDesk Email into Azure AD, you need to add SkyDesk Email from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b4173-125">**To add SkyDesk Email from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b4173-125">**To add SkyDesk Email from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b4173-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b4173-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="b4173-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="b4173-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="b4173-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="b4173-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="b4173-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="b4173-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="b4173-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="b4173-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="b4173-135">In the search box, type **SkyDesk Email**.</span><span class="sxs-lookup"><span data-stu-id="b4173-135">In the search box, type **SkyDesk Email**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_01.png)
7. <span data-ttu-id="b4173-137">In the results pane, select **SkyDesk Email**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="b4173-137">In the results pane, select **SkyDesk Email**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_02.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b4173-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b4173-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="b4173-140">The objective of this section is to show you how to configure and test Azure AD SSO with SkyDesk Email based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b4173-140">The objective of this section is to show you how to configure and test Azure AD SSO with SkyDesk Email based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b4173-141">For SSO to work, Azure AD needs to know what the counterpart user in SkyDesk Email to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="b4173-141">For SSO to work, Azure AD needs to know what the counterpart user in SkyDesk Email to an user in Azure AD is.</span></span> <span data-ttu-id="b4173-142">In other words, a link relationship between an Azure AD user and the related user in SkyDesk Email needs to be established.</span><span class="sxs-lookup"><span data-stu-id="b4173-142">In other words, a link relationship between an Azure AD user and the related user in SkyDesk Email needs to be established.</span></span>

<span data-ttu-id="b4173-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="b4173-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SkyDesk Email.</span></span>

<span data-ttu-id="b4173-144">To configure and test Azure AD SSO with SkyDesk Email, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b4173-144">To configure and test Azure AD SSO with SkyDesk Email, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b4173-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="b4173-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b4173-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b4173-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b4173-147">**[Creating aSkyDesk Email test user](#creating-a-Skydesk-Email-test-user)** - to have a counterpart of Britta Simon in SkyDesk Email that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="b4173-147">**[Creating aSkyDesk Email test user](#creating-a-Skydesk-Email-test-user)** - to have a counterpart of Britta Simon in SkyDesk Email that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="b4173-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b4173-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b4173-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="b4173-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b4173-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b4173-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="b4173-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your SkyDesk Email application.</span><span class="sxs-lookup"><span data-stu-id="b4173-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure single sign-on in your SkyDesk Email application.</span></span>

<span data-ttu-id="b4173-152">**To configure Azure AD single sign-on with SkyDesk Email, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b4173-152">**To configure Azure AD single sign-on with SkyDesk Email, perform the following steps:**</span></span>

1. <span data-ttu-id="b4173-153">In the Azure classic portal, on the **SkyDesk Email** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="b4173-153">In the Azure classic portal, on the **SkyDesk Email** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="b4173-155">On the **How would you like users to sign on to SkyDesk Email** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b4173-155">On the **How would you like users to sign on to SkyDesk Email** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_03.png) 
3. <span data-ttu-id="b4173-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b4173-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_04.png) 

   1. <span data-ttu-id="b4173-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your SkyDesk Email application using the following pattern: **“https://mail.skydesk.jp/portal/\<company name\>”**.</span><span class="sxs-lookup"><span data-stu-id="b4173-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your SkyDesk Email application using the following pattern: **“https://mail.skydesk.jp/portal/\<company name\>”**.</span></span>
   2. <span data-ttu-id="b4173-160">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b4173-160">Click **Next**.</span></span>

4. <span data-ttu-id="b4173-161">On the **Configure single sign-on at SkyDesk Email** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b4173-161">On the **Configure single sign-on at SkyDesk Email** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_05.png) 
   
  1. <span data-ttu-id="b4173-163">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="b4173-163">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="b4173-164">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b4173-164">Click **Next**.</span></span>
5. <span data-ttu-id="b4173-165">To enable SSO in **SkyDesk Email**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b4173-165">To enable SSO in **SkyDesk Email**, perform the following steps:</span></span>
  1. <span data-ttu-id="b4173-166">Sign-on to your SkyDesk Email account as administrator.</span><span class="sxs-lookup"><span data-stu-id="b4173-166">Sign-on to your SkyDesk Email account as administrator.</span></span>
  2. <span data-ttu-id="b4173-167">In the menu on the top, click Setup, and select Org.</span><span class="sxs-lookup"><span data-stu-id="b4173-167">In the menu on the top, click Setup, and select Org.</span></span> 
    
      ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_51.png)  
  3. <span data-ttu-id="b4173-169">Click on Domains from the left panel.</span><span class="sxs-lookup"><span data-stu-id="b4173-169">Click on Domains from the left panel.</span></span>
    
      ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_53.png)
  4. <span data-ttu-id="b4173-171">Click on Add Domain.</span><span class="sxs-lookup"><span data-stu-id="b4173-171">Click on Add Domain.</span></span>
    
      ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_54.png)
  5. <span data-ttu-id="b4173-173">Enter your Domain name, and then verify the Domain.</span><span class="sxs-lookup"><span data-stu-id="b4173-173">Enter your Domain name, and then verify the Domain.</span></span>
    
      ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_55.png)
  6. <span data-ttu-id="b4173-175">Click on **SAML Authentication** from the left panel.</span><span class="sxs-lookup"><span data-stu-id="b4173-175">Click on **SAML Authentication** from the left panel.</span></span>
    
      ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_52.png)
6. <span data-ttu-id="b4173-177">On the **SAML Authentication** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b4173-177">On the **SAML Authentication** dialog page, perform the following steps:</span></span>
   
      ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    ><span data-ttu-id="b4173-179">To use SAML based authentication, you should either have **verified domain** or **portal URL** setup.</span><span class="sxs-lookup"><span data-stu-id="b4173-179">To use SAML based authentication, you should either have **verified domain** or **portal URL** setup.</span></span> <span data-ttu-id="b4173-180">You can set the portal URL with the unique name.</span><span class="sxs-lookup"><span data-stu-id="b4173-180">You can set the portal URL with the unique name.</span></span>
    > 
    > 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_57.png)

   1. <span data-ttu-id="b4173-182">In Azure AD classic portal, copy the **SAML SSO URL** value, and then paste it into the **Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="b4173-182">In Azure AD classic portal, copy the **SAML SSO URL** value, and then paste it into the **Login URL** textbox.</span></span>
   2. <span data-ttu-id="b4173-183">In Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Logout** URL textbox.</span><span class="sxs-lookup"><span data-stu-id="b4173-183">In Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Logout** URL textbox.</span></span>
   3. <span data-ttu-id="b4173-184">**Change Password URL** is optional so leave it blank.</span><span class="sxs-lookup"><span data-stu-id="b4173-184">**Change Password URL** is optional so leave it blank.</span></span>
   4. <span data-ttu-id="b4173-185">Click on **Get Key From File** to select your downloaded SkyDesk Email certificate, and then click **Open** to upload the certificate.</span><span class="sxs-lookup"><span data-stu-id="b4173-185">Click on **Get Key From File** to select your downloaded SkyDesk Email certificate, and then click **Open** to upload the certificate.</span></span>
   5. <span data-ttu-id="b4173-186">As **Algorithm**, select **RSA**.</span><span class="sxs-lookup"><span data-stu-id="b4173-186">As **Algorithm**, select **RSA**.</span></span>
   6. <span data-ttu-id="b4173-187">Click **Ok** to save the changes.</span><span class="sxs-lookup"><span data-stu-id="b4173-187">Click **Ok** to save the changes.</span></span>

7. <span data-ttu-id="b4173-188">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b4173-188">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
8. <span data-ttu-id="b4173-190">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="b4173-190">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b4173-192">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b4173-192">Create an Azure AD test user</span></span>
<span data-ttu-id="b4173-193">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b4173-193">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="b4173-195">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b4173-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b4173-196">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b4173-196">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="b4173-198">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="b4173-198">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="b4173-199">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="b4173-199">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="b4173-201">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="b4173-201">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="b4173-203">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b4173-203">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="b4173-205">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="b4173-205">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="b4173-206">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b4173-206">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="b4173-207">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b4173-207">Click **Next**.</span></span>
6. <span data-ttu-id="b4173-208">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b4173-208">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/create_aaduser_06.png) 
   
   1. <span data-ttu-id="b4173-210">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="b4173-210">In the **First Name** textbox, type **Britta**.</span></span> 
   2. <span data-ttu-id="b4173-211">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="b4173-211">In the **Last Name** textbox, type, **Simon**.</span></span>  
   3. <span data-ttu-id="b4173-212">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b4173-212">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   4. <span data-ttu-id="b4173-213">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="b4173-213">In the **Role** list, select **User**.</span></span>
   5. <span data-ttu-id="b4173-214">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="b4173-214">Click **Next**.</span></span>
7. <span data-ttu-id="b4173-215">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="b4173-215">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="b4173-217">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b4173-217">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/create_aaduser_08.png) 
   
   1. <span data-ttu-id="b4173-219">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="b4173-219">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="b4173-220">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="b4173-220">Click **Complete**.</span></span>   

### <a name="create-a-skydesk-email-test-user"></a><span data-ttu-id="b4173-221">Create a SkyDesk Email test user</span><span class="sxs-lookup"><span data-stu-id="b4173-221">Create a SkyDesk Email test user</span></span>
<span data-ttu-id="b4173-222">In this section, you create a user called Britta Simon in SkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="b4173-222">In this section, you create a user called Britta Simon in SkyDesk Email.</span></span>

1. <span data-ttu-id="b4173-223">Click on **User Access** from the left panel in SkyDesk Email and then enter your username.</span><span class="sxs-lookup"><span data-stu-id="b4173-223">Click on **User Access** from the left panel in SkyDesk Email and then enter your username.</span></span> 

![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
><span data-ttu-id="b4173-225">If you need to create bulk users, you need to contact the SkyDesk Email support team.</span><span class="sxs-lookup"><span data-stu-id="b4173-225">If you need to create bulk users, you need to contact the SkyDesk Email support team.</span></span>
>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b4173-226">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b4173-226">Assign the Azure AD test user</span></span>
<span data-ttu-id="b4173-227">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to SkyDesk Email.</span><span class="sxs-lookup"><span data-stu-id="b4173-227">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to SkyDesk Email.</span></span>

![Assign User][200] 

<span data-ttu-id="b4173-229">**To assign Britta Simon to SkyDesk Email, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b4173-229">**To assign Britta Simon to SkyDesk Email, perform the following steps:**</span></span>

1. <span data-ttu-id="b4173-230">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="b4173-230">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="b4173-232">In the applications list, select **SkyDesk Email**.</span><span class="sxs-lookup"><span data-stu-id="b4173-232">In the applications list, select **SkyDesk Email**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_50.png) 
3. <span data-ttu-id="b4173-234">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="b4173-234">In the menu on the top, click **Users**.</span></span>
<span data-ttu-id="b4173-235">![Assign User][203]</span><span class="sxs-lookup"><span data-stu-id="b4173-235">![Assign User][203]</span></span> 
4. <span data-ttu-id="b4173-236">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b4173-236">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="b4173-237">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="b4173-237">In the toolbar on the bottom, click **Assign**.</span></span>
   
   ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="b4173-239">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="b4173-239">Test single sign-on</span></span>
<span data-ttu-id="b4173-240">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b4173-240">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="b4173-241">When you click the SkyDesk Email tile in the Access Panel, you should get automatically signed-on to your SkyDesk Email application.</span><span class="sxs-lookup"><span data-stu-id="b4173-241">When you click the SkyDesk Email tile in the Access Panel, you should get automatically signed-on to your SkyDesk Email application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b4173-242">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="b4173-242">Additional Resources</span></span>
* [<span data-ttu-id="b4173-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b4173-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b4173-244">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b4173-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-skydeskemail-tutorial/tutorial_general_205.png

































