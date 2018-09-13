---
title: 'Tutorial: Azure Active Directory integration with Birst Agile Business Analytics | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Birst Agile Business Analytics.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 677183b1-5348-4302-88cc-5c8ab63a3c6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: f135bc149f1bd78c2b2dd14e9d75c5a65cff606f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563903"
---
# <a name="tutorial-azure-active-directory-integration-with-birst-agile-business-analytics"></a><span data-ttu-id="baf0d-103">Tutorial: Azure Active Directory integration with Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="baf0d-103">Tutorial: Azure Active Directory integration with Birst Agile Business Analytics</span></span>
<span data-ttu-id="baf0d-104">The objective of this tutorial is to show you how to integrate Birst Agile Business Analytics with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="baf0d-104">The objective of this tutorial is to show you how to integrate Birst Agile Business Analytics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="baf0d-105">Integrating Birst Agile Business Analytics with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="baf0d-105">Integrating Birst Agile Business Analytics with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="baf0d-106">You can control in Azure AD who has access to Birst Agile Business Analytics</span><span class="sxs-lookup"><span data-stu-id="baf0d-106">You can control in Azure AD who has access to Birst Agile Business Analytics</span></span>
* <span data-ttu-id="baf0d-107">You can enable your users to automatically get signed-on to Birst Agile Business Analytics single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="baf0d-107">You can enable your users to automatically get signed-on to Birst Agile Business Analytics single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="baf0d-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="baf0d-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="baf0d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="baf0d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="baf0d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="baf0d-110">Prerequisites</span></span>
<span data-ttu-id="baf0d-111">To configure Azure AD integration with Birst Agile Business Analytics, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="baf0d-111">To configure Azure AD integration with Birst Agile Business Analytics, you need the following items:</span></span>

* <span data-ttu-id="baf0d-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="baf0d-112">An Azure AD subscription</span></span>
* <span data-ttu-id="baf0d-113">A Birst Agile Business Analytics SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="baf0d-113">A Birst Agile Business Analytics SSO enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="baf0d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="baf0d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="baf0d-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="baf0d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="baf0d-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="baf0d-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="baf0d-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="baf0d-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="baf0d-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="baf0d-118">Scenario Description</span></span>
<span data-ttu-id="baf0d-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="baf0d-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="baf0d-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="baf0d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="baf0d-121">Adding Birst Agile Business Analytics from the gallery</span><span class="sxs-lookup"><span data-stu-id="baf0d-121">Adding Birst Agile Business Analytics from the gallery</span></span>
2. <span data-ttu-id="baf0d-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="baf0d-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-birst-agile-business-analytics-from-the-gallery"></a><span data-ttu-id="baf0d-123">Add Birst Agile Business Analytics from the gallery</span><span class="sxs-lookup"><span data-stu-id="baf0d-123">Add Birst Agile Business Analytics from the gallery</span></span>
<span data-ttu-id="baf0d-124">To configure the integration of Birst Agile Business Analytics into Azure AD, you need to add Birst Agile Business Analytics from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="baf0d-124">To configure the integration of Birst Agile Business Analytics into Azure AD, you need to add Birst Agile Business Analytics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="baf0d-125">**To add Birst Agile Business Analytics from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="baf0d-125">**To add Birst Agile Business Analytics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="baf0d-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="baf0d-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="baf0d-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="baf0d-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="baf0d-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="baf0d-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="baf0d-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="baf0d-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="baf0d-135">In the search box, type **Birst Agile Business Analytics**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-135">In the search box, type **Birst Agile Business Analytics**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/tutorial_birst_01.png)
7. <span data-ttu-id="baf0d-137">In the results pane, select **Birst Agile Business Analytics**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="baf0d-137">In the results pane, select **Birst Agile Business Analytics**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/tutorial_birst_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="baf0d-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="baf0d-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="baf0d-140">The objective of this section is to show you how to configure and test Azure AD SSO with Birst Agile Business Analytics based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="baf0d-140">The objective of this section is to show you how to configure and test Azure AD SSO with Birst Agile Business Analytics based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="baf0d-141">For SSO to work, Azure AD needs to know what the counterpart user in Birst Agile Business Analytics to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="baf0d-141">For SSO to work, Azure AD needs to know what the counterpart user in Birst Agile Business Analytics to an user in Azure AD is.</span></span> <span data-ttu-id="baf0d-142">In other words, a link relationship between an Azure AD user and the related user in Birst Agile Business Analytics needs to be established.</span><span class="sxs-lookup"><span data-stu-id="baf0d-142">In other words, a link relationship between an Azure AD user and the related user in Birst Agile Business Analytics needs to be established.</span></span>

<span data-ttu-id="baf0d-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="baf0d-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Birst Agile Business Analytics.</span></span>

<span data-ttu-id="baf0d-144">To configure and test Azure AD single sign-on with Birst Agile Business Analytics, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="baf0d-144">To configure and test Azure AD single sign-on with Birst Agile Business Analytics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="baf0d-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="baf0d-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="baf0d-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="baf0d-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="baf0d-147">**[Creating a Birst Agile Business Analytics test user](#creating-a-birst-agile-business-analytics-test-user)** - to have a counterpart of Britta Simon in Birst Agile Business Analytics that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="baf0d-147">**[Creating a Birst Agile Business Analytics test user](#creating-a-birst-agile-business-analytics-test-user)** - to have a counterpart of Britta Simon in Birst Agile Business Analytics that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="baf0d-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="baf0d-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="baf0d-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="baf0d-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="baf0d-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="baf0d-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="baf0d-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Birst Agile Business Analytics application.</span><span class="sxs-lookup"><span data-stu-id="baf0d-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Birst Agile Business Analytics application.</span></span>

<span data-ttu-id="baf0d-152">**To configure Azure AD SSO with Birst Agile Business Analytics, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="baf0d-152">**To configure Azure AD SSO with Birst Agile Business Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="baf0d-153">In the Azure classic portal, on the **Birst Agile Business Analytics** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="baf0d-153">In the Azure classic portal, on the **Birst Agile Business Analytics** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="baf0d-155">On the **How would you like users to sign on to Birst Agile Business Analytics** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-155">On the **How would you like users to sign on to Birst Agile Business Analytics** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/tutorial_birst_03.png) 
3. <span data-ttu-id="baf0d-157">On the **Configure App Settings** dialog page, perform the following steps:.</span><span class="sxs-lookup"><span data-stu-id="baf0d-157">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/tutorial_birst_04.png) 
  1. <span data-ttu-id="baf0d-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your Birst Agile Business Analytics application using the following pattern: “https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID”.</span><span class="sxs-lookup"><span data-stu-id="baf0d-159">In the Sign On URL textbox, type the URL used by your users to sign-on to your Birst Agile Business Analytics application using the following pattern: “https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID”.</span></span>
   <span data-ttu-id="baf0d-160">The URL is dependent on the datacenter that your Birst account is located.</span><span class="sxs-lookup"><span data-stu-id="baf0d-160">The URL is dependent on the datacenter that your Birst account is located.</span></span> <span data-ttu-id="baf0d-161">For US datacenter use “https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID” and for Europe datacenter use “https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID".</span><span class="sxs-lookup"><span data-stu-id="baf0d-161">For US datacenter use “https://login.bws.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID” and for Europe datacenter use “https://login.eu1.birst.com/SAMLSSO/Services.aspx?birst.idpid=TENANTIDPID".</span></span>
  2. <span data-ttu-id="baf0d-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-162">Click **Next**.</span></span>
4. <span data-ttu-id="baf0d-163">On the **Configure single sign-on at Birst Agile Business Analytics** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="baf0d-163">On the **Configure single sign-on at Birst Agile Business Analytics** page, perform the following steps:</span></span>
   
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/tutorial_birst_05.png)   
  1. <span data-ttu-id="baf0d-165">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="baf0d-165">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="baf0d-166">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-166">Click **Next**.</span></span>
5. <span data-ttu-id="baf0d-167">To get SSO configured for your application, contact your Birst Agile Business Analytics support team via [info@birst.com](emailTo:info@birst.com) and attach the downloaded certificate file to your email.</span><span class="sxs-lookup"><span data-stu-id="baf0d-167">To get SSO configured for your application, contact your Birst Agile Business Analytics support team via [info@birst.com](emailTo:info@birst.com) and attach the downloaded certificate file to your email.</span></span> <span data-ttu-id="baf0d-168">Also please do provide the SAML SSO URL, Sign Out URL and Issuer URL so that they can be configured for SSO integration.</span><span class="sxs-lookup"><span data-stu-id="baf0d-168">Also please do provide the SAML SSO URL, Sign Out URL and Issuer URL so that they can be configured for SSO integration.</span></span>

 >[!NOTE]
 ><span data-ttu-id="baf0d-169">Please mention to Birst team that this integration need SHA256 Algorithm (SHA1 will not be supported) so that they can set the SSO on the appropriate server like **app2101** etc.</span><span class="sxs-lookup"><span data-stu-id="baf0d-169">Please mention to Birst team that this integration need SHA256 Algorithm (SHA1 will not be supported) so that they can set the SSO on the appropriate server like **app2101** etc.</span></span>
 >  

6. <span data-ttu-id="baf0d-170">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-170">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="baf0d-172">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-172">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="baf0d-174">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="baf0d-174">Create an Azure AD test user</span></span>
<span data-ttu-id="baf0d-175">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="baf0d-175">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="baf0d-176">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-176">In the Users list, select **Britta Simon**.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="baf0d-178">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="baf0d-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="baf0d-179">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-179">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="baf0d-181">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="baf0d-181">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="baf0d-182">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-182">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="baf0d-184">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-184">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="baf0d-186">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="baf0d-186">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="baf0d-188">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="baf0d-188">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="baf0d-189">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-189">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="baf0d-190">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-190">Click **Next**.</span></span>
6. <span data-ttu-id="baf0d-191">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="baf0d-191">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="baf0d-193">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-193">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="baf0d-194">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-194">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="baf0d-195">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-195">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="baf0d-196">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-196">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="baf0d-197">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-197">Click **Next**.</span></span>
7. <span data-ttu-id="baf0d-198">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-198">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="baf0d-200">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="baf0d-200">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="baf0d-202">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-202">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="baf0d-203">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-203">Click **Complete**.</span></span>   

### <a name="create-a-birst-agile-business-analytics-test-user"></a><span data-ttu-id="baf0d-204">Create a Birst Agile Business Analytics test user</span><span class="sxs-lookup"><span data-stu-id="baf0d-204">Create a Birst Agile Business Analytics test user</span></span>
<span data-ttu-id="baf0d-205">The objective of this section is to create a user called Britta Simon in Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="baf0d-205">The objective of this section is to create a user called Britta Simon in Birst Agile Business Analytics.</span></span> <span data-ttu-id="baf0d-206">Please work with Birst Agile Business Analytics support team to add the users in the Birst account.</span><span class="sxs-lookup"><span data-stu-id="baf0d-206">Please work with Birst Agile Business Analytics support team to add the users in the Birst account.</span></span> 

>[!NOTE]
><span data-ttu-id="baf0d-207">If you need to create an user manually, you need to contact the Birst Agile Business Analytics support team.</span><span class="sxs-lookup"><span data-stu-id="baf0d-207">If you need to create an user manually, you need to contact the Birst Agile Business Analytics support team.</span></span>
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="baf0d-208">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="baf0d-208">Assign the Azure AD test user</span></span>
<span data-ttu-id="baf0d-209">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Birst Agile Business Analytics.</span><span class="sxs-lookup"><span data-stu-id="baf0d-209">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Birst Agile Business Analytics.</span></span>

![Assign User][200] 

<span data-ttu-id="baf0d-211">**To assign Britta Simon to Birst Agile Business Analytics, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="baf0d-211">**To assign Britta Simon to Birst Agile Business Analytics, perform the following steps:**</span></span>

1. <span data-ttu-id="baf0d-212">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="baf0d-212">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="baf0d-214">In the applications list, select **Birst Agile Business Analytics**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-214">In the applications list, select **Birst Agile Business Analytics**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/tutorial_birst_50.png) 
3. <span data-ttu-id="baf0d-216">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-216">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="baf0d-218">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-218">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="baf0d-219">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="baf0d-219">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="baf0d-221">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="baf0d-221">Test single sign-on</span></span>
<span data-ttu-id="baf0d-222">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="baf0d-222">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="baf0d-223">When you click the Birst Agile Business Analytics tile in the Access Panel, you should get automatically signed-on to your Birst Agile Business Analytics application.</span><span class="sxs-lookup"><span data-stu-id="baf0d-223">When you click the Birst Agile Business Analytics tile in the Access Panel, you should get automatically signed-on to your Birst Agile Business Analytics application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="baf0d-224">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="baf0d-224">Additional Resources</span></span>
* [<span data-ttu-id="baf0d-225">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="baf0d-225">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="baf0d-226">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="baf0d-226">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-birst-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-birst-tutorial/tutorial_general_205.png

























