---
title: 'Tutorial: Azure Active Directory integration with Deputy | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Deputy.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: jeedes
ms.openlocfilehash: 0d5b9b5e8079ec9aa61a4e40581bf656132c7815
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551214"
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="29134-103">Tutorial: Azure Active Directory integration with Deputy</span><span class="sxs-lookup"><span data-stu-id="29134-103">Tutorial: Azure Active Directory integration with Deputy</span></span>
<span data-ttu-id="29134-104">The objective of this tutorial is to show you how to integrate Deputy with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="29134-104">The objective of this tutorial is to show you how to integrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="29134-105">Integrating Deputy with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="29134-105">Integrating Deputy with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="29134-106">You can control in Azure AD who has access to Deputy</span><span class="sxs-lookup"><span data-stu-id="29134-106">You can control in Azure AD who has access to Deputy</span></span>
* <span data-ttu-id="29134-107">You can enable your users to automatically get signed-on to Deputy  single sign-on (\*SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="29134-107">You can enable your users to automatically get signed-on to Deputy  single sign-on (\*SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="29134-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="29134-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="29134-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="29134-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29134-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="29134-110">Prerequisites</span></span>
<span data-ttu-id="29134-111">To configure Azure AD integration with Deputy, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="29134-111">To configure Azure AD integration with Deputy, you need the following items:</span></span>

* <span data-ttu-id="29134-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="29134-112">An Azure AD subscription</span></span>
* <span data-ttu-id="29134-113">A Deputy single sign-on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="29134-113">A Deputy single sign-on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="29134-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="29134-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="29134-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="29134-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="29134-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="29134-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="29134-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29134-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="29134-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="29134-118">Scenario description</span></span>
<span data-ttu-id="29134-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="29134-119">The objective of this tutorial is to enable you to test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="29134-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="29134-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="29134-121">Adding Deputy from the gallery</span><span class="sxs-lookup"><span data-stu-id="29134-121">Adding Deputy from the gallery</span></span>
2. <span data-ttu-id="29134-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="29134-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-deputy-from-the-gallery"></a><span data-ttu-id="29134-123">Adding Deputy from the gallery</span><span class="sxs-lookup"><span data-stu-id="29134-123">Adding Deputy from the gallery</span></span>
<span data-ttu-id="29134-124">To configure the integration of Deputy into Azure AD, you need to add Deputy from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="29134-124">To configure the integration of Deputy into Azure AD, you need to add Deputy from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="29134-125">**To add Deputy from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="29134-125">**To add Deputy from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="29134-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29134-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="29134-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="29134-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="29134-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="29134-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="29134-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="29134-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="29134-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="29134-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="29134-135">In the search box, type **Deputy**.</span><span class="sxs-lookup"><span data-stu-id="29134-135">In the search box, type **Deputy**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_deputy_01.png)
7. <span data-ttu-id="29134-137">In the results panel, select **Deputy**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="29134-137">In the results panel, select **Deputy**, and then click **Complete** to add the application.</span></span>
   
    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_deputy_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="29134-139">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="29134-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="29134-140">The objective of this section is to show you how to configure and test Azure AD SSO with Deputy based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="29134-140">The objective of this section is to show you how to configure and test Azure AD SSO with Deputy based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="29134-141">For SSO to work, Azure AD needs to know what the counterpart user in Deputy to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="29134-141">For SSO to work, Azure AD needs to know what the counterpart user in Deputy to an user in Azure AD is.</span></span> <span data-ttu-id="29134-142">In other words, a link relationship between an Azure AD user and the related user in Deputy needs to be established.</span><span class="sxs-lookup"><span data-stu-id="29134-142">In other words, a link relationship between an Azure AD user and the related user in Deputy needs to be established.</span></span>

<span data-ttu-id="29134-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Deputy.</span><span class="sxs-lookup"><span data-stu-id="29134-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Deputy.</span></span>

<span data-ttu-id="29134-144">To configure and test Azure AD SSO with Deputy, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="29134-144">To configure and test Azure AD SSO with Deputy, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="29134-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="29134-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="29134-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29134-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="29134-147">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - to have a counterpart of Britta Simon in Deputy that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="29134-147">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - to have a counterpart of Britta Simon in Deputy that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="29134-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="29134-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="29134-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="29134-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="29134-150">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="29134-150">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="29134-151">In this section, you enable Azure AD single sign-on in the classic portal and configure SSO in your Deputy application.</span><span class="sxs-lookup"><span data-stu-id="29134-151">In this section, you enable Azure AD single sign-on in the classic portal and configure SSO in your Deputy application.</span></span>

<span data-ttu-id="29134-152">**To configure Azure AD single sign-on with Deputy, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="29134-152">**To configure Azure AD single sign-on with Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="29134-153">In the classic portal, on the **Deputy** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog.</span><span class="sxs-lookup"><span data-stu-id="29134-153">In the classic portal, on the **Deputy** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On** dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="29134-155">On the **How would you like users to sign on to Deputy** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="29134-155">On the **How would you like users to sign on to Deputy** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_deputy_03.png)
3. <span data-ttu-id="29134-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="29134-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_deputy_04.png)
  1. <span data-ttu-id="29134-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<your-subdomain>.<region>.deputy.com`.</span><span class="sxs-lookup"><span data-stu-id="29134-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<your-subdomain>.<region>.deputy.com`.</span></span>
  2. <span data-ttu-id="29134-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.<region>.deputy.com/exec/devapp/samlacs`.</span><span class="sxs-lookup"><span data-stu-id="29134-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.<region>.deputy.com/exec/devapp/samlacs`.</span></span>
  3. <span data-ttu-id="29134-161">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="29134-161">Click **Next**.</span></span>
4. <span data-ttu-id="29134-162">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="29134-162">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_deputy_05.png)
   1. <span data-ttu-id="29134-164">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.<region>.deputy.com`.</span><span class="sxs-lookup"><span data-stu-id="29134-164">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.<region>.deputy.com`.</span></span>
   2. <span data-ttu-id="29134-165">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="29134-165">Click **Next**.</span></span>
   
     >[!NOTE]
     > <span data-ttu-id="29134-166">Deputy region suffix is opitional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span><span class="sxs-lookup"><span data-stu-id="29134-166">Deputy region suffix is opitional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>
     > 

5. <span data-ttu-id="29134-167">On the **Configure single sign-on at Deputy** page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="29134-167">On the **Configure single sign-on at Deputy** page, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_deputy_06.png)
   *  <span data-ttu-id="29134-169">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="29134-169">Click **Download certificate**, and then save the file on your computer.</span></span>
6. <span data-ttu-id="29134-170">Navigate to the following URL: https://(your-subdomain).deputy.com/exec/config/system_config.</span><span class="sxs-lookup"><span data-stu-id="29134-170">Navigate to the following URL: https://(your-subdomain).deputy.com/exec/config/system_config.</span></span> <span data-ttu-id="29134-171">Go to **Security Settings** and click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="29134-171">Go to **Security Settings** and click **Edit**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)
7. <span data-ttu-id="29134-173">In the Azure classic portal, on the Configure single sign-on at Deputy page, copy the SAML SSO URL.</span><span class="sxs-lookup"><span data-stu-id="29134-173">In the Azure classic portal, on the Configure single sign-on at Deputy page, copy the SAML SSO URL.</span></span> 
8. <span data-ttu-id="29134-174">On this **Security Settings** page, perform below steps.</span><span class="sxs-lookup"><span data-stu-id="29134-174">On this **Security Settings** page, perform below steps.</span></span>
   
![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)

   1. <span data-ttu-id="29134-176">Enable **Social Login**.</span><span class="sxs-lookup"><span data-stu-id="29134-176">Enable **Social Login**.</span></span>
   2. <span data-ttu-id="29134-177">Open your Base64 encoded certificate in notepad, copy the content of it nto your clipboard, and then paste it to the **OpenSSL Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="29134-177">Open your Base64 encoded certificate in notepad, copy the content of it nto your clipboard, and then paste it to the **OpenSSL Certificate** textbox.</span></span>
   3. <span data-ttu-id="29134-178">In the SAM SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span><span class="sxs-lookup"><span data-stu-id="29134-178">In the SAM SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
   4. <span data-ttu-id="29134-179">In the SAM SSO URL textbox, replace `<your subdomain>` with your subdomain.</span><span class="sxs-lookup"><span data-stu-id="29134-179">In the SAM SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   5. <span data-ttu-id="29134-180">In the SAM SSO URL textbox, replace `<saml sso url>` with the SAML SSO URL you have copied from the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="29134-180">In the SAM SSO URL textbox, replace `<saml sso url>` with the SAML SSO URL you have copied from the Azure classic portal.</span></span>
   6. <span data-ttu-id="29134-181">Click **Save Settings**.</span><span class="sxs-lookup"><span data-stu-id="29134-181">Click **Save Settings**.</span></span>
9. <span data-ttu-id="29134-182">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="29134-182">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
10. <span data-ttu-id="29134-184">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="29134-184">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="29134-186">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="29134-186">Create an Azure AD test user</span></span>
<span data-ttu-id="29134-187">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29134-187">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="29134-189">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="29134-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="29134-190">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29134-190">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="29134-192">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="29134-192">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="29134-193">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="29134-193">To display the list of users, in the menu on the top, click **Users**.</span></span>
       <span data-ttu-id="29134-194">![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/create_aaduser_03.png)</span><span class="sxs-lookup"><span data-stu-id="29134-194">![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/create_aaduser_03.png)</span></span>
4. <span data-ttu-id="29134-195">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="29134-195">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="29134-197">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="29134-197">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/create_aaduser_05.png)

   1. <span data-ttu-id="29134-199">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="29134-199">As Type Of User, select New user in your organization.</span></span>
   2. <span data-ttu-id="29134-200">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="29134-200">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   3. <span data-ttu-id="29134-201">Click **Next**.6.</span><span class="sxs-lookup"><span data-stu-id="29134-201">Click **Next**.6.</span></span> <span data-ttu-id="29134-202">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="29134-202">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/create_aaduser_06.png)
   
   1. <span data-ttu-id="29134-204">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="29134-204">In the **First Name** textbox, type **Britta**.</span></span>  
   2. <span data-ttu-id="29134-205">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="29134-205">In the **Last Name** textbox, type, **Simon**.</span></span>
   3. <span data-ttu-id="29134-206">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="29134-206">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   4. <span data-ttu-id="29134-207">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="29134-207">In the **Role** list, select **User**.</span></span>
   5. <span data-ttu-id="29134-208">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="29134-208">Click **Next**.</span></span>
   
7. <span data-ttu-id="29134-209">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="29134-209">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="29134-211">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="29134-211">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/create_aaduser_08.png)
   
   1. <span data-ttu-id="29134-213">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="29134-213">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="29134-214">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="29134-214">Click **Complete**.</span></span>   

### <a name="create-a-deputy-test-user"></a><span data-ttu-id="29134-215">Create a Deputy test user</span><span class="sxs-lookup"><span data-stu-id="29134-215">Create a Deputy test user</span></span>
<span data-ttu-id="29134-216">In order to enable Azure AD users to log into Deputy, they must be provisioned into Deputy.</span><span class="sxs-lookup"><span data-stu-id="29134-216">In order to enable Azure AD users to log into Deputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="29134-217">In the case of Deputy, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="29134-217">In the case of Deputy, provisioning is a manual task.</span></span>

#### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="29134-218">To provision a user account, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="29134-218">To provision a user account, perform the following steps:</span></span>
1. <span data-ttu-id="29134-219">Log into your Deputy company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="29134-219">Log into your Deputy company site as an administrator.</span></span>
2. <span data-ttu-id="29134-220">On the top navigation pane, click **People**.</span><span class="sxs-lookup"><span data-stu-id="29134-220">On the top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="29134-221">![People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span><span class="sxs-lookup"><span data-stu-id="29134-221">![People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span></span>
3. <span data-ttu-id="29134-222">Click the **Add People** button and click **Add a single person**.</span><span class="sxs-lookup"><span data-stu-id="29134-222">Click the **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="29134-223">![Add People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span><span class="sxs-lookup"><span data-stu-id="29134-223">![Add People](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>
4. <span data-ttu-id="29134-224">Perform the following steps and click **Save & Invite**.</span><span class="sxs-lookup"><span data-stu-id="29134-224">Perform the following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="29134-225">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span><span class="sxs-lookup"><span data-stu-id="29134-225">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>
   
  1. <span data-ttu-id="29134-226">In the **Name** textbox, type **Britta** and **Simon**.</span><span class="sxs-lookup"><span data-stu-id="29134-226">In the **Name** textbox, type **Britta** and **Simon**.</span></span>  
  2. <span data-ttu-id="29134-227">In the **Email** textbox, type the email address of an Azure AD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="29134-227">In the **Email** textbox, type the email address of an Azure AD account you want to provision.</span></span>
  3. <span data-ttu-id="29134-228">In the **Work at** textbox, type the bussniess name.</span><span class="sxs-lookup"><span data-stu-id="29134-228">In the **Work at** textbox, type the bussniess name.</span></span>
  4. <span data-ttu-id="29134-229">Click **Save & Invite** button.</span><span class="sxs-lookup"><span data-stu-id="29134-229">Click **Save & Invite** button.</span></span>

5. <span data-ttu-id="29134-230">The AAD account holder will receive an email and follow a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="29134-230">The AAD account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span> <span data-ttu-id="29134-231">You can use any other Deputy user account creation tools or APIs provided by Deputy to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="29134-231">You can use any other Deputy user account creation tools or APIs provided by Deputy to provision AAD user accounts.</span></span>
    
### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="29134-232">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="29134-232">Assign the Azure AD test user</span></span>
<span data-ttu-id="29134-233">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Deputy.</span><span class="sxs-lookup"><span data-stu-id="29134-233">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Deputy.</span></span>

![Assign User][200]

<span data-ttu-id="29134-235">**To assign Britta Simon to Deputy, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="29134-235">**To assign Britta Simon to Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="29134-236">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="29134-236">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201]
2. <span data-ttu-id="29134-238">In the applications list, select **Deputy**.</span><span class="sxs-lookup"><span data-stu-id="29134-238">In the applications list, select **Deputy**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_deputy_50.png)
3. <span data-ttu-id="29134-240">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="29134-240">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="29134-242">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="29134-242">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="29134-243">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="29134-243">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="29134-245">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="29134-245">Test single sign-on</span></span>
<span data-ttu-id="29134-246">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="29134-246">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="29134-247">When you click the Deputy tile in the Access Panel, you should get automatically signed-on to your Deputy application.</span><span class="sxs-lookup"><span data-stu-id="29134-247">When you click the Deputy tile in the Access Panel, you should get automatically signed-on to your Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="29134-248">Additional resources</span><span class="sxs-lookup"><span data-stu-id="29134-248">Additional resources</span></span>
* [<span data-ttu-id="29134-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29134-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="29134-250">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="29134-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-deputy-tutorial/tutorial_general_205.png































