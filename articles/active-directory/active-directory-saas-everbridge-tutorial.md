---
title: 'Tutorial: Azure Active Directory integration with Everbridge | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Everbridge.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 58d7cd22-98c0-4606-9ce5-8bdb22ee8b3e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 23ff3ed0e615ee85edc0d5bdd1031604419b7028
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662654"
---
# <a name="tutorial-azure-active-directory-integration-with-everbridge"></a><span data-ttu-id="8f696-103">Tutorial: Azure Active Directory integration with EverBridge</span><span class="sxs-lookup"><span data-stu-id="8f696-103">Tutorial: Azure Active Directory integration with EverBridge</span></span>
<span data-ttu-id="8f696-104">The objective of this tutorial is to show you how to integrate Everbridge with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8f696-104">The objective of this tutorial is to show you how to integrate Everbridge with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8f696-105">Integrating Everbridge with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8f696-105">Integrating Everbridge with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="8f696-106">You can control in Azure AD who has access to Everbridge</span><span class="sxs-lookup"><span data-stu-id="8f696-106">You can control in Azure AD who has access to Everbridge</span></span>
* <span data-ttu-id="8f696-107">You can enable your users to automatically get signed-on to Everbridge (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="8f696-107">You can enable your users to automatically get signed-on to Everbridge (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="8f696-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="8f696-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="8f696-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8f696-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f696-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8f696-110">Prerequisites</span></span>
<span data-ttu-id="8f696-111">To configure Azure AD integration with Everbridge, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8f696-111">To configure Azure AD integration with Everbridge, you need the following items:</span></span>

* <span data-ttu-id="8f696-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8f696-112">An Azure AD subscription</span></span>
* <span data-ttu-id="8f696-113">A Everbridge single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8f696-113">A Everbridge single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8f696-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8f696-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="8f696-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8f696-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="8f696-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="8f696-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="8f696-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8f696-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8f696-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="8f696-118">Scenario Description</span></span>
<span data-ttu-id="8f696-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8f696-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="8f696-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8f696-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8f696-121">Adding Everbridge from the gallery</span><span class="sxs-lookup"><span data-stu-id="8f696-121">Adding Everbridge from the gallery</span></span>
2. <span data-ttu-id="8f696-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8f696-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-everbridge-from-the-gallery"></a><span data-ttu-id="8f696-123">Adding Everbridge from the gallery</span><span class="sxs-lookup"><span data-stu-id="8f696-123">Adding Everbridge from the gallery</span></span>
<span data-ttu-id="8f696-124">To configure the integration of Everbridge into Azure AD, you need to add Everbridge from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8f696-124">To configure the integration of Everbridge into Azure AD, you need to add Everbridge from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8f696-125">**To add Everbridge from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8f696-125">**To add Everbridge from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8f696-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8f696-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="8f696-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="8f696-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="8f696-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="8f696-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="8f696-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="8f696-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="8f696-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="8f696-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="8f696-135">In the search box, type **Everbridge**.</span><span class="sxs-lookup"><span data-stu-id="8f696-135">In the search box, type **Everbridge**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_01.png)
7. <span data-ttu-id="8f696-137">In the results pane, select **Everbridge**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="8f696-137">In the results pane, select **Everbridge**, and then click **Complete** to add the application.</span></span>
   
    ![Selecting the app in the gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_001.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8f696-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8f696-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8f696-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Everbridge based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8f696-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Everbridge based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8f696-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Everbridge to an user in Azure AD is.</span><span class="sxs-lookup"><span data-stu-id="8f696-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Everbridge to an user in Azure AD is.</span></span> <span data-ttu-id="8f696-142">In other words, a link relationship between an Azure AD user and the related user in Everbridge needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8f696-142">In other words, a link relationship between an Azure AD user and the related user in Everbridge needs to be established.</span></span>

<span data-ttu-id="8f696-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Everbridge.</span><span class="sxs-lookup"><span data-stu-id="8f696-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Everbridge.</span></span>

<span data-ttu-id="8f696-144">To configure and test Azure AD single sign-on with Everbridge, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8f696-144">To configure and test Azure AD single sign-on with Everbridge, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8f696-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8f696-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8f696-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8f696-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8f696-147">**[Creating a Everbridge test user](#creating-a-everbridge-test-user)** - to have a counterpart of Britta Simon in Everbridge that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="8f696-147">**[Creating a Everbridge test user](#creating-a-everbridge-test-user)** - to have a counterpart of Britta Simon in Everbridge that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="8f696-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8f696-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8f696-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8f696-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8f696-150">Configuring Azure AD Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8f696-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="8f696-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Everbridge application.</span><span class="sxs-lookup"><span data-stu-id="8f696-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Everbridge application.</span></span>

<span data-ttu-id="8f696-152">**To configure Azure AD single sign-on with Everbridge, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8f696-152">**To configure Azure AD single sign-on with Everbridge, perform the following steps:**</span></span>

1. <span data-ttu-id="8f696-153">In the classic portal, on the **Everbridge** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="8f696-153">In the classic portal, on the **Everbridge** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="8f696-155">On the **How would you like users to sign on to Everbridge** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8f696-155">On the **How would you like users to sign on to Everbridge** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_03.png) 
3. <span data-ttu-id="8f696-157">On the **Configure App Settings** dialog page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="8f696-157">On the **Configure App Settings** dialog page, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_04.png)
   
    <span data-ttu-id="8f696-159">a.</span><span class="sxs-lookup"><span data-stu-id="8f696-159">a.</span></span> <span data-ttu-id="8f696-160">In the **Identifier** textbox, type the URL using the following pattern: `https://sso.everbridge.net/{<company name>}`</span><span class="sxs-lookup"><span data-stu-id="8f696-160">In the **Identifier** textbox, type the URL using the following pattern: `https://sso.everbridge.net/{<company name>}`</span></span>
   
    <span data-ttu-id="8f696-161">b.</span><span class="sxs-lookup"><span data-stu-id="8f696-161">b.</span></span> <span data-ttu-id="8f696-162">In the **Reply URL** textbox, type the URL using the following pattern: `https://manager.everbridge.net/saml/SSO/{<company name>}/alias/defaultAlias`</span><span class="sxs-lookup"><span data-stu-id="8f696-162">In the **Reply URL** textbox, type the URL using the following pattern: `https://manager.everbridge.net/saml/SSO/{<company name>}/alias/defaultAlias`</span></span>
   
    <span data-ttu-id="8f696-163">c.</span><span class="sxs-lookup"><span data-stu-id="8f696-163">c.</span></span> <span data-ttu-id="8f696-164">Click **Next**</span><span class="sxs-lookup"><span data-stu-id="8f696-164">Click **Next**</span></span>
4. <span data-ttu-id="8f696-165">On the **Configure single sign-on at Everbridge** page, perform the following steps and click **Next**:</span><span class="sxs-lookup"><span data-stu-id="8f696-165">On the **Configure single sign-on at Everbridge** page, perform the following steps and click **Next**:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_05.png)
   
    <span data-ttu-id="8f696-167">a.</span><span class="sxs-lookup"><span data-stu-id="8f696-167">a.</span></span> <span data-ttu-id="8f696-168">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8f696-168">Click **Download metadata**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="8f696-169">b.</span><span class="sxs-lookup"><span data-stu-id="8f696-169">b.</span></span> <span data-ttu-id="8f696-170">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8f696-170">Click **Next**.</span></span>
5. <span data-ttu-id="8f696-171">To get SSO configured for your application, you need to sign-on to your Everbridge tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="8f696-171">To get SSO configured for your application, you need to sign-on to your Everbridge tenant as an administrator.</span></span>
6. <span data-ttu-id="8f696-172">In the menu on the top, click the **Settings** tab and select **Single Sign-On** under **Security**.</span><span class="sxs-lookup"><span data-stu-id="8f696-172">In the menu on the top, click the **Settings** tab and select **Single Sign-On** under **Security**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_002.png)
   
    <span data-ttu-id="8f696-174">a.</span><span class="sxs-lookup"><span data-stu-id="8f696-174">a.</span></span> <span data-ttu-id="8f696-175">In the **Name** textbox, type the name of Identifier Provider (e.g.: your company name).</span><span class="sxs-lookup"><span data-stu-id="8f696-175">In the **Name** textbox, type the name of Identifier Provider (e.g.: your company name).</span></span>
   
    <span data-ttu-id="8f696-176">b.</span><span class="sxs-lookup"><span data-stu-id="8f696-176">b.</span></span> <span data-ttu-id="8f696-177">In the **API Name** textbox, type the name of API.</span><span class="sxs-lookup"><span data-stu-id="8f696-177">In the **API Name** textbox, type the name of API.</span></span>
   
    <span data-ttu-id="8f696-178">C.</span><span class="sxs-lookup"><span data-stu-id="8f696-178">C.</span></span> <span data-ttu-id="8f696-179">Click **Choose File** button to upload the metadata file which you downloaded in **Step 4**.</span><span class="sxs-lookup"><span data-stu-id="8f696-179">Click **Choose File** button to upload the metadata file which you downloaded in **Step 4**.</span></span>
   
    <span data-ttu-id="8f696-180">d.</span><span class="sxs-lookup"><span data-stu-id="8f696-180">d.</span></span> <span data-ttu-id="8f696-181">As **SAML Identity Location**, select "Identity is in the NameIdentifier element of the Subject statement".</span><span class="sxs-lookup"><span data-stu-id="8f696-181">As **SAML Identity Location**, select "Identity is in the NameIdentifier element of the Subject statement".</span></span>
   
    <span data-ttu-id="8f696-182">e.</span><span class="sxs-lookup"><span data-stu-id="8f696-182">e.</span></span> <span data-ttu-id="8f696-183">Copy SAML SSO URL from Azure AD to **Identity Provider Login URL** in Everbridge.</span><span class="sxs-lookup"><span data-stu-id="8f696-183">Copy SAML SSO URL from Azure AD to **Identity Provider Login URL** in Everbridge.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_003.png)
   
    <span data-ttu-id="8f696-185">f.</span><span class="sxs-lookup"><span data-stu-id="8f696-185">f.</span></span> <span data-ttu-id="8f696-186">As **Service Provider Initiated Request Binding**, select HTTP Redirect.</span><span class="sxs-lookup"><span data-stu-id="8f696-186">As **Service Provider Initiated Request Binding**, select HTTP Redirect.</span></span>
7. <span data-ttu-id="8f696-187">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8f696-187">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
8. <span data-ttu-id="8f696-189">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="8f696-189">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8f696-191">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8f696-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="8f696-192">The objective of this section is to create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8f696-192">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

<span data-ttu-id="8f696-193">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8f696-193">In the Users list, select **Britta Simon**.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="8f696-195">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8f696-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8f696-196">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8f696-196">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="8f696-198">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="8f696-198">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="8f696-199">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="8f696-199">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="8f696-201">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="8f696-201">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="8f696-203">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8f696-203">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/create_aaduser_05.png)
   
    <span data-ttu-id="8f696-205">a.</span><span class="sxs-lookup"><span data-stu-id="8f696-205">a.</span></span> <span data-ttu-id="8f696-206">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="8f696-206">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="8f696-207">b.</span><span class="sxs-lookup"><span data-stu-id="8f696-207">b.</span></span> <span data-ttu-id="8f696-208">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8f696-208">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="8f696-209">c.</span><span class="sxs-lookup"><span data-stu-id="8f696-209">c.</span></span> <span data-ttu-id="8f696-210">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8f696-210">Click **Next**.</span></span>
6. <span data-ttu-id="8f696-211">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8f696-211">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/create_aaduser_06.png)
   
    <span data-ttu-id="8f696-213">a.</span><span class="sxs-lookup"><span data-stu-id="8f696-213">a.</span></span> <span data-ttu-id="8f696-214">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="8f696-214">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="8f696-215">b.</span><span class="sxs-lookup"><span data-stu-id="8f696-215">b.</span></span> <span data-ttu-id="8f696-216">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="8f696-216">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="8f696-217">c.</span><span class="sxs-lookup"><span data-stu-id="8f696-217">c.</span></span> <span data-ttu-id="8f696-218">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8f696-218">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="8f696-219">d.</span><span class="sxs-lookup"><span data-stu-id="8f696-219">d.</span></span> <span data-ttu-id="8f696-220">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="8f696-220">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="8f696-221">e.</span><span class="sxs-lookup"><span data-stu-id="8f696-221">e.</span></span> <span data-ttu-id="8f696-222">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="8f696-222">Click **Next**.</span></span>

7. <span data-ttu-id="8f696-223">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="8f696-223">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="8f696-225">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8f696-225">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/create_aaduser_08.png)
   
    <span data-ttu-id="8f696-227">a.</span><span class="sxs-lookup"><span data-stu-id="8f696-227">a.</span></span> <span data-ttu-id="8f696-228">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="8f696-228">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="8f696-229">b.</span><span class="sxs-lookup"><span data-stu-id="8f696-229">b.</span></span> <span data-ttu-id="8f696-230">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="8f696-230">Click **Complete**.</span></span>   

### <a name="creating-a-everbridge-test-user"></a><span data-ttu-id="8f696-231">Creating a Everbridge test user</span><span class="sxs-lookup"><span data-stu-id="8f696-231">Creating a Everbridge test user</span></span>
<span data-ttu-id="8f696-232">In this section, you create a user called Britta Simon in Everbridge.</span><span class="sxs-lookup"><span data-stu-id="8f696-232">In this section, you create a user called Britta Simon in Everbridge.</span></span> <span data-ttu-id="8f696-233">Please work with Everbridge support team via <mailto:support@everbridge.com> to add the users in the Everbridge platform.</span><span class="sxs-lookup"><span data-stu-id="8f696-233">Please work with Everbridge support team via <mailto:support@everbridge.com> to add the users in the Everbridge platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8f696-234">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8f696-234">Assigning the Azure AD test user</span></span>
<span data-ttu-id="8f696-235">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Everbridge.</span><span class="sxs-lookup"><span data-stu-id="8f696-235">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Everbridge.</span></span>

![Assign User][200]

<span data-ttu-id="8f696-237">**To assign Britta Simon to Everbridge, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8f696-237">**To assign Britta Simon to Everbridge, perform the following steps:**</span></span>

1. <span data-ttu-id="8f696-238">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="8f696-238">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201]
2. <span data-ttu-id="8f696-240">In the applications list, select **Everbridge**.</span><span class="sxs-lookup"><span data-stu-id="8f696-240">In the applications list, select **Everbridge**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/tutorial_everbridge_50.png)
3. <span data-ttu-id="8f696-242">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="8f696-242">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="8f696-244">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8f696-244">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="8f696-245">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="8f696-245">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="8f696-247">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="8f696-247">Testing Single Sign-On</span></span>
<span data-ttu-id="8f696-248">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8f696-248">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8f696-249">When you click the Everbridge tile in the Access Panel, you should get automatically signed-on to your Everbridge application.</span><span class="sxs-lookup"><span data-stu-id="8f696-249">When you click the Everbridge tile in the Access Panel, you should get automatically signed-on to your Everbridge application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8f696-250">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="8f696-250">Additional Resources</span></span>
* [<span data-ttu-id="8f696-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8f696-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8f696-252">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8f696-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-everbridge-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-everbridge-tutorial/tutorial_general_205.png



























