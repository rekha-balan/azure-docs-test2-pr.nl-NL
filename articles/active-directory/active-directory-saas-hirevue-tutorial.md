---
title: 'Tutorial: Azure Active Directory integration with HireVue | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and HireVue.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: aadfc342-14db-4d74-a83d-f0c76f0cf63c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: d9ec256c4cd501800ddbab6f2af68c95daeb2c7b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554178"
---
# <a name="tutorial-azure-active-directory-integration-with-hirevue"></a><span data-ttu-id="ae89b-103">Tutorial: Azure Active Directory integration with HireVue</span><span class="sxs-lookup"><span data-stu-id="ae89b-103">Tutorial: Azure Active Directory integration with HireVue</span></span>
<span data-ttu-id="ae89b-104">In this tutorial, you learn how to integrate HireVue with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae89b-104">In this tutorial, you learn how to integrate HireVue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae89b-105">Integrating HireVue with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ae89b-105">Integrating HireVue with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="ae89b-106">You can control in Azure AD who has access to HireVue</span><span class="sxs-lookup"><span data-stu-id="ae89b-106">You can control in Azure AD who has access to HireVue</span></span>
* <span data-ttu-id="ae89b-107">You can enable your users to automatically get signed-on to HireVue single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="ae89b-107">You can enable your users to automatically get signed-on to HireVue single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="ae89b-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="ae89b-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="ae89b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ae89b-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae89b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ae89b-110">Prerequisites</span></span>
<span data-ttu-id="ae89b-111">To configure Azure AD integration with HireVue, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="ae89b-111">To configure Azure AD integration with HireVue, you need the following items:</span></span>

* <span data-ttu-id="ae89b-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="ae89b-112">An Azure AD subscription</span></span>
* <span data-ttu-id="ae89b-113">A HireVue single-sign on (SSO) enabled subscription</span><span class="sxs-lookup"><span data-stu-id="ae89b-113">A HireVue single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="ae89b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="ae89b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="ae89b-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="ae89b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="ae89b-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="ae89b-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="ae89b-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae89b-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae89b-118">Scenario Description</span><span class="sxs-lookup"><span data-stu-id="ae89b-118">Scenario Description</span></span>
<span data-ttu-id="ae89b-119">In this tutorial, you test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="ae89b-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="ae89b-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="ae89b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae89b-121">Adding HireVue from the gallery</span><span class="sxs-lookup"><span data-stu-id="ae89b-121">Adding HireVue from the gallery</span></span>
2. <span data-ttu-id="ae89b-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="ae89b-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-hirevue-from-the-gallery"></a><span data-ttu-id="ae89b-123">Add HireVue from the gallery</span><span class="sxs-lookup"><span data-stu-id="ae89b-123">Add HireVue from the gallery</span></span>
<span data-ttu-id="ae89b-124">To configure the integration of HireVue into Azure AD, you need to add HireVue from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="ae89b-124">To configure the integration of HireVue into Azure AD, you need to add HireVue from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ae89b-125">**To add HireVue from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae89b-125">**To add HireVue from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ae89b-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]
2. <span data-ttu-id="ae89b-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="ae89b-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ae89b-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="ae89b-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="ae89b-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="ae89b-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="ae89b-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="ae89b-135">In the search box, type **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-135">In the search box, type **HireVue**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_01.png)
7. <span data-ttu-id="ae89b-137">In the results pane, select **HireVue**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="ae89b-137">In the results pane, select **HireVue**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_06.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="ae89b-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="ae89b-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="ae89b-140">In this section, you configure and test Azure AD SSO with HireVue based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="ae89b-140">In this section, you configure and test Azure AD SSO with HireVue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ae89b-141">For SSO to work, Azure AD needs to know what the counterpart user in HireVue is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae89b-141">For SSO to work, Azure AD needs to know what the counterpart user in HireVue is to a user in Azure AD.</span></span> <span data-ttu-id="ae89b-142">In other words, a link relationship between an Azure AD user and the related user in HireVue needs to be established.</span><span class="sxs-lookup"><span data-stu-id="ae89b-142">In other words, a link relationship between an Azure AD user and the related user in HireVue needs to be established.</span></span>

<span data-ttu-id="ae89b-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in HireVue.</span><span class="sxs-lookup"><span data-stu-id="ae89b-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in HireVue.</span></span>

<span data-ttu-id="ae89b-144">To configure and test Azure AD single sign-on with HireVue, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="ae89b-144">To configure and test Azure AD single sign-on with HireVue, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ae89b-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="ae89b-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ae89b-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae89b-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ae89b-147">**[Creating a HireVue test user](#creating-a-predictix-price-reporting-test-user)** - to have a counterpart of Britta Simon in HireVue that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="ae89b-147">**[Creating a HireVue test user](#creating-a-predictix-price-reporting-test-user)** - to have a counterpart of Britta Simon in HireVue that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="ae89b-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="ae89b-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ae89b-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="ae89b-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="ae89b-150">Configure Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="ae89b-150">Configure Azure AD SSO</span></span>
<span data-ttu-id="ae89b-151">In this section, you enable Azure AD single sign-on in the classic portal and configure SSO in your HireVue application.</span><span class="sxs-lookup"><span data-stu-id="ae89b-151">In this section, you enable Azure AD single sign-on in the classic portal and configure SSO in your HireVue application.</span></span>

<span data-ttu-id="ae89b-152">**To configure Azure AD SSO with HireVue, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae89b-152">**To configure Azure AD SSO with HireVue, perform the following steps:**</span></span>

1. <span data-ttu-id="ae89b-153">In the classic portal, on the **HireVue** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="ae89b-153">In the classic portal, on the **HireVue** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 
2. <span data-ttu-id="ae89b-155">On the **How would you like users to sign on to HireVue** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-155">On the **How would you like users to sign on to HireVue** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_03.png) 
3. <span data-ttu-id="ae89b-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ae89b-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_04.png) 
  1. <span data-ttu-id="ae89b-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your HireVue application using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="ae89b-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your HireVue application using the following pattern:</span></span> 

    | <span data-ttu-id="ae89b-160">Environment</span><span class="sxs-lookup"><span data-stu-id="ae89b-160">Environment</span></span> | <span data-ttu-id="ae89b-161">URL</span><span class="sxs-lookup"><span data-stu-id="ae89b-161">URL</span></span> |
    |---|---|
    | <span data-ttu-id="ae89b-162">Production</span><span class="sxs-lookup"><span data-stu-id="ae89b-162">Production</span></span> | `https://<company name>.hirevue.com` |
    | <span data-ttu-id="ae89b-163">Staging</span><span class="sxs-lookup"><span data-stu-id="ae89b-163">Staging</span></span>| `https://<company name>.stghv.com` |
  2. <span data-ttu-id="ae89b-164">In the **Identifier** textbox, type the URN using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="ae89b-164">In the **Identifier** textbox, type the URN using the following pattern:</span></span>
  
    | <span data-ttu-id="ae89b-165">Environment</span><span class="sxs-lookup"><span data-stu-id="ae89b-165">Environment</span></span> | <span data-ttu-id="ae89b-166">URN</span><span class="sxs-lookup"><span data-stu-id="ae89b-166">URN</span></span> |
    |---|---|
    |<span data-ttu-id="ae89b-167">Production</span><span class="sxs-lookup"><span data-stu-id="ae89b-167">Production</span></span> | `urn:federation:hirevue.com:saml:sp:prod` |
    |<span data-ttu-id="ae89b-168">Staging</span><span class="sxs-lookup"><span data-stu-id="ae89b-168">Staging</span></span> | `urn:federation:hirevue.com:saml:sp:staging` |
  3. <span data-ttu-id="ae89b-169">click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-169">click **Next**.</span></span>

4. <span data-ttu-id="ae89b-170">On the **Configure single sign-on at HireVue** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ae89b-170">On the **Configure single sign-on at HireVue** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_05.png)  
  1. <span data-ttu-id="ae89b-172">Click **Download certificate**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="ae89b-172">Click **Download certificate**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="ae89b-173">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-173">Click **Next**.</span></span>
5. <span data-ttu-id="ae89b-174">To get SSO configured for your application, contact HireVue support team at [samlsupport@hirevue.com](mailTo:samlsupport@hirevue.com) and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="ae89b-174">To get SSO configured for your application, contact HireVue support team at [samlsupport@hirevue.com](mailTo:samlsupport@hirevue.com) and provide them with the following:</span></span>

  * <span data-ttu-id="ae89b-175">The downloaded **certificate**</span><span class="sxs-lookup"><span data-stu-id="ae89b-175">The downloaded **certificate**</span></span>  
  * <span data-ttu-id="ae89b-176">The **Entity ID**</span><span class="sxs-lookup"><span data-stu-id="ae89b-176">The **Entity ID**</span></span>
  * <span data-ttu-id="ae89b-177">The **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="ae89b-177">The **SAML SSO URL**</span></span>   
  * <span data-ttu-id="ae89b-178">The **Single Sign Out Service URL**</span><span class="sxs-lookup"><span data-stu-id="ae89b-178">The **Single Sign Out Service URL**</span></span>
6. <span data-ttu-id="ae89b-179">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-179">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="ae89b-181">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-181">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ae89b-183">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ae89b-183">Create an Azure AD test user</span></span>
<span data-ttu-id="ae89b-184">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae89b-184">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="ae89b-186">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae89b-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ae89b-187">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-187">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="ae89b-189">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="ae89b-189">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ae89b-190">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-190">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="ae89b-192">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-192">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="ae89b-194">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ae89b-194">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="ae89b-196">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="ae89b-196">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="ae89b-197">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-197">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="ae89b-198">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-198">Click **Next**.</span></span>
6. <span data-ttu-id="ae89b-199">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ae89b-199">On the **User Profile** dialog page, perform the following steps:</span></span>

   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="ae89b-201">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-201">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="ae89b-202">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-202">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="ae89b-203">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-203">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="ae89b-204">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-204">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="ae89b-205">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-205">Click **Next**.</span></span>
7. <span data-ttu-id="ae89b-206">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-206">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="ae89b-208">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="ae89b-208">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="ae89b-210">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-210">Write down the value of the **New Password**.</span></span> 
  2. <span data-ttu-id="ae89b-211">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-211">Click **Complete**.</span></span>   

### <a name="create-an-hirevue-test-user"></a><span data-ttu-id="ae89b-212">Create an HireVue test user</span><span class="sxs-lookup"><span data-stu-id="ae89b-212">Create an HireVue test user</span></span>
<span data-ttu-id="ae89b-213">In this section, you create a user called Britta Simon in HireVue.</span><span class="sxs-lookup"><span data-stu-id="ae89b-213">In this section, you create a user called Britta Simon in HireVue.</span></span> <span data-ttu-id="ae89b-214">Please work with HireVue support team to add the users in the HireVue platform.</span><span class="sxs-lookup"><span data-stu-id="ae89b-214">Please work with HireVue support team to add the users in the HireVue platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ae89b-215">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="ae89b-215">Assign the Azure AD test user</span></span>
<span data-ttu-id="ae89b-216">In this section, you enable Britta Simon to use Azure SSO by granting her access to HireVue.</span><span class="sxs-lookup"><span data-stu-id="ae89b-216">In this section, you enable Britta Simon to use Azure SSO by granting her access to HireVue.</span></span>

![Assign User][200] 

<span data-ttu-id="ae89b-218">**To assign Britta Simon to HireVue, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="ae89b-218">**To assign Britta Simon to HireVue, perform the following steps:**</span></span>

1. <span data-ttu-id="ae89b-219">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="ae89b-219">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="ae89b-221">In the applications list, select **HireVue**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-221">In the applications list, select **HireVue**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/tutorial_hirevue_50.png) 
3. <span data-ttu-id="ae89b-223">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-223">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]
4. <span data-ttu-id="ae89b-225">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-225">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="ae89b-226">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="ae89b-226">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="ae89b-228">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="ae89b-228">Test single sign-on</span></span>
<span data-ttu-id="ae89b-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="ae89b-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ae89b-230">When you click the HireVue tile in the Access Panel, you should get automatically signed-on to your HireVue application.</span><span class="sxs-lookup"><span data-stu-id="ae89b-230">When you click the HireVue tile in the Access Panel, you should get automatically signed-on to your HireVue application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ae89b-231">Additional Resources</span><span class="sxs-lookup"><span data-stu-id="ae89b-231">Additional Resources</span></span>
* [<span data-ttu-id="ae89b-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae89b-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ae89b-233">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ae89b-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-hirevue-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-hirevue-tutorial/tutorial_general_205.png

























