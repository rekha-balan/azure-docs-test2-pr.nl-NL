---
title: 'Tutorial: Azure Active Directory integration with &frankly | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and &frankly.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 1d702060-1b89-4e9d-9f01-ede4f1171c73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: jeedes
ms.openlocfilehash: daacd6337c1f42b5d642a8932cd54fbf8190faef
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555677"
---
# <a name="tutorial-azure-active-directory-integration-with-frankly"></a><span data-ttu-id="1eeba-103">Tutorial: Azure Active Directory integration with &frankly</span><span class="sxs-lookup"><span data-stu-id="1eeba-103">Tutorial: Azure Active Directory integration with &frankly</span></span>
<span data-ttu-id="1eeba-104">The objective of this tutorial is to show you how to integrate &frankly with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1eeba-104">The objective of this tutorial is to show you how to integrate &frankly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1eeba-105">Integrating &frankly with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1eeba-105">Integrating &frankly with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="1eeba-106">You can control in Azure AD who has access to &frankly</span><span class="sxs-lookup"><span data-stu-id="1eeba-106">You can control in Azure AD who has access to &frankly</span></span>
* <span data-ttu-id="1eeba-107">You can enable your users to automatically get signed-on to &frankly single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="1eeba-107">You can enable your users to automatically get signed-on to &frankly single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="1eeba-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="1eeba-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="1eeba-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1eeba-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1eeba-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1eeba-110">Prerequisites</span></span>
<span data-ttu-id="1eeba-111">To configure Azure AD integration with &frankly, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1eeba-111">To configure Azure AD integration with &frankly, you need the following items:</span></span>

* <span data-ttu-id="1eeba-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="1eeba-112">An Azure AD subscription</span></span>
* <span data-ttu-id="1eeba-113">A &frankly single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1eeba-113">A &frankly single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="1eeba-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1eeba-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="1eeba-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1eeba-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="1eeba-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="1eeba-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="1eeba-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1eeba-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1eeba-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="1eeba-118">Scenario description</span></span>
<span data-ttu-id="1eeba-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1eeba-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="1eeba-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1eeba-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1eeba-121">Adding &frankly from the gallery</span><span class="sxs-lookup"><span data-stu-id="1eeba-121">Adding &frankly from the gallery</span></span>
2. <span data-ttu-id="1eeba-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="1eeba-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-frankly-from-the-gallery"></a><span data-ttu-id="1eeba-123">Adding &frankly from the gallery</span><span class="sxs-lookup"><span data-stu-id="1eeba-123">Adding &frankly from the gallery</span></span>
<span data-ttu-id="1eeba-124">To configure the integration of &frankly into Azure AD, you need to add &frankly from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1eeba-124">To configure the integration of &frankly into Azure AD, you need to add &frankly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1eeba-125">**To add &frankly from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1eeba-125">**To add &frankly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1eeba-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="1eeba-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1eeba-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1eeba-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1eeba-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="1eeba-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1eeba-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="1eeba-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="1eeba-135">In the search box, type **&frankly**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-135">In the search box, type **&frankly**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_01.png)
7. <span data-ttu-id="1eeba-137">In the results panel, select **&frankly**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="1eeba-137">In the results panel, select **&frankly**, and then click **Complete** to add the application.</span></span>
   
    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_0001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="1eeba-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="1eeba-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="1eeba-140">The objective of this section is to show you how to configure and test Azure AD SSO with &frankly based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1eeba-140">The objective of this section is to show you how to configure and test Azure AD SSO with &frankly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1eeba-141">For SSO to work, Azure AD needs to know what the counterpart user in &frankly to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="1eeba-141">For SSO to work, Azure AD needs to know what the counterpart user in &frankly to an user in Azure AD is.</span></span> <span data-ttu-id="1eeba-142">In other words, a link relationship between an Azure AD user and the related user in &frankly needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1eeba-142">In other words, a link relationship between an Azure AD user and the related user in &frankly needs to be established.</span></span>

<span data-ttu-id="1eeba-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in &frankly.</span><span class="sxs-lookup"><span data-stu-id="1eeba-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in &frankly.</span></span>

<span data-ttu-id="1eeba-144">To configure and test Azure AD single sign-on with &frankly, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1eeba-144">To configure and test Azure AD single sign-on with &frankly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1eeba-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1eeba-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1eeba-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1eeba-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1eeba-147">**[Creating a &frankly test user](#creating-a-&frankly-test-user)** - to have a counterpart of Britta Simon in &frankly that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="1eeba-147">**[Creating a &frankly test user](#creating-a-&frankly-test-user)** - to have a counterpart of Britta Simon in &frankly that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="1eeba-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1eeba-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1eeba-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1eeba-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="1eeba-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="1eeba-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="1eeba-151">In this section, you enable Azure AD single sign-on in the classic portal and configure SSO in your &frankly application.</span><span class="sxs-lookup"><span data-stu-id="1eeba-151">In this section, you enable Azure AD single sign-on in the classic portal and configure SSO in your &frankly application.</span></span>

<span data-ttu-id="1eeba-152">**To configure Azure AD SSO with &frankly, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1eeba-152">**To configure Azure AD SSO with &frankly, perform the following steps:**</span></span>

1. <span data-ttu-id="1eeba-153">In the classic portal, on the **&frankly** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="1eeba-153">In the classic portal, on the **&frankly** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="1eeba-155">On the **How would you like users to sign on to &frankly** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-155">On the **How would you like users to sign on to &frankly** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_03.png)
3. <span data-ttu-id="1eeba-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="1eeba-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_04.png)
  1. <span data-ttu-id="1eeba-159">In the **Identifier** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="1eeba-159">In the **Identifier** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span></span>
  2. <span data-ttu-id="1eeba-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="1eeba-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span></span>
  3. <span data-ttu-id="1eeba-161">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-161">Click **Next**.</span></span>
4. <span data-ttu-id="1eeba-162">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-162">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_05.png)
  1. <span data-ttu-id="1eeba-164">In the **Sign On URL** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="1eeba-164">In the **Sign On URL** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span></span>
  2. <span data-ttu-id="1eeba-165">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-165">Click **Next**.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="1eeba-166">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="1eeba-166">Please note that these are not the real values.</span></span> <span data-ttu-id="1eeba-167">You have to update these values with the actual Sign On URL, Identifier and Reply URL.Contact [help@andfrankly.com](emailTo:help@andfrankly.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="1eeba-167">You have to update these values with the actual Sign On URL, Identifier and Reply URL.Contact [help@andfrankly.com](emailTo:help@andfrankly.com) to get these values.</span></span>
   >  
5. <span data-ttu-id="1eeba-168">On the **Configure single sign-on at &frankly** page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="1eeba-168">On the **Configure single sign-on at &frankly** page, perform the following steps and click **Next**:</span></span>
   
 ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_06.png)
 1. <span data-ttu-id="1eeba-170">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="1eeba-170">Click **Download certificate**, and then save the file on your computer.</span></span> 
 2. <span data-ttu-id="1eeba-171">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-171">Click **Next**.</span></span>
6. <span data-ttu-id="1eeba-172">To get SSO configured for your application, contact your &frankly support team via [help@andfrankly.com](emailTo:help@andfrankly.com).</span><span class="sxs-lookup"><span data-stu-id="1eeba-172">To get SSO configured for your application, contact your &frankly support team via [help@andfrankly.com](emailTo:help@andfrankly.com).</span></span> <span data-ttu-id="1eeba-173">Attach the downloaded metadata file and share it with &frankly team to set up SSO on their side.</span><span class="sxs-lookup"><span data-stu-id="1eeba-173">Attach the downloaded metadata file and share it with &frankly team to set up SSO on their side.</span></span>
7. <span data-ttu-id="1eeba-174">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-174">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
8. <span data-ttu-id="1eeba-176">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-176">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1eeba-178">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1eeba-178">Create an Azure AD test user</span></span>
<span data-ttu-id="1eeba-179">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1eeba-179">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="1eeba-181">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1eeba-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1eeba-182">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-182">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="1eeba-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1eeba-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1eeba-185">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-185">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="1eeba-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="1eeba-189">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1eeba-189">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/create_aaduser_05.png)
 1. <span data-ttu-id="1eeba-191">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="1eeba-191">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="1eeba-192">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-192">In the User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="1eeba-193">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-193">Click **Next**.</span></span>
6. <span data-ttu-id="1eeba-194">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1eeba-194">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/create_aaduser_06.png) 
 1. <span data-ttu-id="1eeba-196">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-196">In the **First Name** textbox, type **Britta**.</span></span>   
 2. <span data-ttu-id="1eeba-197">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-197">In the **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="1eeba-198">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-198">In the **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="1eeba-199">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-199">In the **Role** list, select **User**.</span></span> 
 5. <span data-ttu-id="1eeba-200">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-200">Click **Next**.</span></span>
7. <span data-ttu-id="1eeba-201">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-201">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="1eeba-203">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1eeba-203">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/create_aaduser_08.png) 
 1. <span data-ttu-id="1eeba-205">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-205">Write down the value of the **New Password**.</span></span> 
 2. <span data-ttu-id="1eeba-206">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-206">Click **Complete**.</span></span>   

### <a name="create-a-frankly-test-user"></a><span data-ttu-id="1eeba-207">Create a &frankly test user</span><span class="sxs-lookup"><span data-stu-id="1eeba-207">Create a &frankly test user</span></span>
<span data-ttu-id="1eeba-208">In this section, you create a user called Britta Simon in &frankly.</span><span class="sxs-lookup"><span data-stu-id="1eeba-208">In this section, you create a user called Britta Simon in &frankly.</span></span> <span data-ttu-id="1eeba-209">Please work with &frankly support team via [help@andfrankly.com](emailTo:help@andfrankly.com) to add the users in the &frankly platform.</span><span class="sxs-lookup"><span data-stu-id="1eeba-209">Please work with &frankly support team via [help@andfrankly.com](emailTo:help@andfrankly.com) to add the users in the &frankly platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1eeba-210">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1eeba-210">Assign the Azure AD test user</span></span>
<span data-ttu-id="1eeba-211">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to &frankly.</span><span class="sxs-lookup"><span data-stu-id="1eeba-211">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to &frankly.</span></span>

![Assign User][200]

<span data-ttu-id="1eeba-213">**To assign Britta Simon to &frankly, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1eeba-213">**To assign Britta Simon to &frankly, perform the following steps:**</span></span>

1. <span data-ttu-id="1eeba-214">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1eeba-214">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201]
2. <span data-ttu-id="1eeba-216">In the applications list, select **&frankly**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-216">In the applications list, select **&frankly**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_50.png)
3. <span data-ttu-id="1eeba-218">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-218">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="1eeba-220">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-220">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="1eeba-221">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="1eeba-221">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="1eeba-223">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="1eeba-223">Test single sign-on</span></span>
<span data-ttu-id="1eeba-224">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1eeba-224">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="1eeba-225">When you click the &frankly tile in the Access Panel, you should get automatically signed-on to your &frankly application.</span><span class="sxs-lookup"><span data-stu-id="1eeba-225">When you click the &frankly tile in the Access Panel, you should get automatically signed-on to your &frankly application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1eeba-226">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1eeba-226">Additional resources</span></span>
* [<span data-ttu-id="1eeba-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1eeba-227">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1eeba-228">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1eeba-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-andfrankly-tutorial/tutorial_general_205.png


























