---
title: 'Tutorial: Azure Active Directory integration with Tableau Online | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Tableau Online.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: 1d4b1149-ba3b-4f4e-8bce-9791316b730d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: 0977169f4965bae9a6458f3d52c0051c7b64e5f0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550161"
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-online"></a><span data-ttu-id="1fcf7-103">Tutorial: Azure Active Directory integration with Tableau Online</span><span class="sxs-lookup"><span data-stu-id="1fcf7-103">Tutorial: Azure Active Directory integration with Tableau Online</span></span>
<span data-ttu-id="1fcf7-104">In this tutorial, you learn how to integrate Tableau Online with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1fcf7-104">In this tutorial, you learn how to integrate Tableau Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1fcf7-105">Integrating Tableau Online with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="1fcf7-105">Integrating Tableau Online with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="1fcf7-106">You can control in Azure AD who has access to Tableau Online</span><span class="sxs-lookup"><span data-stu-id="1fcf7-106">You can control in Azure AD who has access to Tableau Online</span></span>
* <span data-ttu-id="1fcf7-107">You can enable your users to automatically get signed-on to Tableau Online single sign-on (SSO) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="1fcf7-107">You can enable your users to automatically get signed-on to Tableau Online single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="1fcf7-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="1fcf7-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="1fcf7-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1fcf7-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1fcf7-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1fcf7-110">Prerequisites</span></span>
<span data-ttu-id="1fcf7-111">To configure Azure AD integration with Tableau Online, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="1fcf7-111">To configure Azure AD integration with Tableau Online, you need the following items:</span></span>

* <span data-ttu-id="1fcf7-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="1fcf7-112">An Azure AD subscription</span></span>
* <span data-ttu-id="1fcf7-113">A **Tableau Online** SSO enabled subscription</span><span class="sxs-lookup"><span data-stu-id="1fcf7-113">A **Tableau Online** SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="1fcf7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="1fcf7-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="1fcf7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="1fcf7-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="1fcf7-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1fcf7-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1fcf7-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="1fcf7-118">Scenario description</span></span>
<span data-ttu-id="1fcf7-119">In this tutorial, you test Azure AD SSO in a test environment.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="1fcf7-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="1fcf7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1fcf7-121">Adding Tableau Online from the gallery</span><span class="sxs-lookup"><span data-stu-id="1fcf7-121">Adding Tableau Online from the gallery</span></span>
2. <span data-ttu-id="1fcf7-122">Configuring and testing Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="1fcf7-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-tableau-online-from-the-gallery"></a><span data-ttu-id="1fcf7-123">Adding Tableau Online from the gallery</span><span class="sxs-lookup"><span data-stu-id="1fcf7-123">Adding Tableau Online from the gallery</span></span>
<span data-ttu-id="1fcf7-124">To configure the integration of Tableau Online into Azure AD, you need to add Tableau Online from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-124">To configure the integration of Tableau Online into Azure AD, you need to add Tableau Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1fcf7-125">**To add Tableau Online from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1fcf7-125">**To add Tableau Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1fcf7-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="1fcf7-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1fcf7-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="1fcf7-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="1fcf7-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="1fcf7-135">In the search box, type **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-135">In the search box, type **Tableau Online**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_01.png)
7. <span data-ttu-id="1fcf7-137">In the results pane, select **Tableau Online**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-137">In the results pane, select **Tableau Online**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_02.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="1fcf7-139">Configure and test Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="1fcf7-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="1fcf7-140">In this section, you configure and test Azure AD SSO with Tableau Online based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="1fcf7-140">In this section, you configure and test Azure AD SSO with Tableau Online based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1fcf7-141">For SSO to work, Azure AD needs to know what the counterpart user in Tableau Online is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-141">For SSO to work, Azure AD needs to know what the counterpart user in Tableau Online is to a user in Azure AD.</span></span> <span data-ttu-id="1fcf7-142">In other words, a link relationship between an Azure AD user and the related user in Tableau Online needs to be established.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-142">In other words, a link relationship between an Azure AD user and the related user in Tableau Online needs to be established.</span></span>

<span data-ttu-id="1fcf7-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Tableau Online.</span></span>

<span data-ttu-id="1fcf7-144">To configure and test Azure AD SSO with Tableau Online, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="1fcf7-144">To configure and test Azure AD SSO with Tableau Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1fcf7-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1fcf7-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1fcf7-147">**[Creating a Tableau Online test user](#creating-a-Tableau-Online-test-user)** - to have a counterpart of Britta Simon in Tableau Online that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-147">**[Creating a Tableau Online test user](#creating-a-Tableau-Online-test-user)** - to have a counterpart of Britta Simon in Tableau Online that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="1fcf7-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1fcf7-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="1fcf7-150">Configuring Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="1fcf7-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="1fcf7-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Tableau Online application.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-151">The objective of this section is to enable Azure AD SSO in the Azure classic portal and to configure SSO in your Tableau Online application.</span></span>

<span data-ttu-id="1fcf7-152">**To configure Azure AD SSO with Tableau Online, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1fcf7-152">**To configure Azure AD SSO with Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="1fcf7-153">In the menu on the top, click **Quick Start**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-153">In the menu on the top, click **Quick Start**.</span></span>
   
    ![Configure Single Sign-On][6]
2. <span data-ttu-id="1fcf7-155">In the classic portal, on the **Tableau Online** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-155">In the classic portal, on the **Tableau Online** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][7] 
3. <span data-ttu-id="1fcf7-157">On the **How would you like users to sign on to Tableau Online** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-157">On the **How would you like users to sign on to Tableau Online** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_06.png)
4. <span data-ttu-id="1fcf7-159">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1fcf7-159">On the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_07.png)
  1. <span data-ttu-id="1fcf7-161">In the Sign On URL textbox, type a URL using the following pattern: `https://sso.online.tableau.com`</span><span class="sxs-lookup"><span data-stu-id="1fcf7-161">In the Sign On URL textbox, type a URL using the following pattern: `https://sso.online.tableau.com`</span></span>
  2. <span data-ttu-id="1fcf7-162">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-162">Click **Next**.</span></span>
5. <span data-ttu-id="1fcf7-163">On the **Configure single sign-on at Tableau Online** page, Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-163">On the **Configure single sign-on at Tableau Online** page, Click **Download metadata**, and then save the file on your computer.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_08.png)
6. <span data-ttu-id="1fcf7-165">Select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-165">Select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]
7. <span data-ttu-id="1fcf7-167">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-167">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]
8. <span data-ttu-id="1fcf7-169">In a different browser window, sign-on to your Tableau Online application.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-169">In a different browser window, sign-on to your Tableau Online application.</span></span> <span data-ttu-id="1fcf7-170">Go to **Settings** and then **Authentication**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-170">Go to **Settings** and then **Authentication**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_09.png)
9. <span data-ttu-id="1fcf7-172">Under **Authentication Types** section.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-172">Under **Authentication Types** section.</span></span> <span data-ttu-id="1fcf7-173">Check the **Single sign-on with SAML** checkbox to enable SAML.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-173">Check the **Single sign-on with SAML** checkbox to enable SAML.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_12.png)
10. <span data-ttu-id="1fcf7-175">Scroll down until **Import metadata file into Tableau Online** section.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-175">Scroll down until **Import metadata file into Tableau Online** section.</span></span>  <span data-ttu-id="1fcf7-176">Click Browse and import the metadata file you have downloaded from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-176">Click Browse and import the metadata file you have downloaded from Azure AD.</span></span> <span data-ttu-id="1fcf7-177">Then, click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-177">Then, click **Apply**.</span></span>
   
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_13.png)
11. <span data-ttu-id="1fcf7-179">In the **Match assertions** section, insert the corresponding Identity Provider assertion name for email address, first name and last name.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-179">In the **Match assertions** section, insert the corresponding Identity Provider assertion name for email address, first name and last name.</span></span> <span data-ttu-id="1fcf7-180">To get this information from Azure AD:</span><span class="sxs-lookup"><span data-stu-id="1fcf7-180">To get this information from Azure AD:</span></span> 
  1. <span data-ttu-id="1fcf7-181">Go back to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-181">Go back to Azure AD.</span></span> <span data-ttu-id="1fcf7-182">In the Azure classic portal, on the **Tableau Online** application integration page.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-182">In the Azure classic portal, on the **Tableau Online** application integration page.</span></span>
  2. <span data-ttu-id="1fcf7-183">On the menu on the top, click **Attributes**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-183">On the menu on the top, click **Attributes**.</span></span> 
  3. <span data-ttu-id="1fcf7-184">Copy the name for the values: userprincipalname, givenname and surname.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-184">Copy the name for the values: userprincipalname, givenname and surname.</span></span>
   
     ![Azure AD Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_10.png)
  4. <span data-ttu-id="1fcf7-186">Switch to the Tableau Online application, then set the **Tableau Online Attributes** section as follow:</span><span class="sxs-lookup"><span data-stu-id="1fcf7-186">Switch to the Tableau Online application, then set the **Tableau Online Attributes** section as follow:</span></span>
     * <span data-ttu-id="1fcf7-187">Email: **mail** or **userprincipalname**</span><span class="sxs-lookup"><span data-stu-id="1fcf7-187">Email: **mail** or **userprincipalname**</span></span>
     * <span data-ttu-id="1fcf7-188">First name: **givenname**</span><span class="sxs-lookup"><span data-stu-id="1fcf7-188">First name: **givenname**</span></span>
     * <span data-ttu-id="1fcf7-189">Last name: **surname**</span><span class="sxs-lookup"><span data-stu-id="1fcf7-189">Last name: **surname**</span></span>
   
   ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_14.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1fcf7-191">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1fcf7-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="1fcf7-192">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-192">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="1fcf7-194">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1fcf7-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1fcf7-195">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-195">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/create_aaduser_09.png) 
2. <span data-ttu-id="1fcf7-197">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-197">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="1fcf7-198">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-198">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="1fcf7-200">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-200">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="1fcf7-202">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1fcf7-202">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="1fcf7-204">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-204">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="1fcf7-205">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-205">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="1fcf7-206">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-206">Click **Next**.</span></span>
6. <span data-ttu-id="1fcf7-207">On the **User Profile** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1fcf7-207">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="1fcf7-209">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-209">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="1fcf7-210">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-210">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="1fcf7-211">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-211">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="1fcf7-212">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-212">In the **Role** list, select **User**.</span></span> 
  5. <span data-ttu-id="1fcf7-213">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-213">Click **Next**.</span></span>
7. <span data-ttu-id="1fcf7-214">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-214">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="1fcf7-216">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1fcf7-216">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="1fcf7-218">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-218">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="1fcf7-219">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-219">Click **Complete**.</span></span>   

### <a name="create-a-tableau-online-test-user"></a><span data-ttu-id="1fcf7-220">Create a Tableau Online test user</span><span class="sxs-lookup"><span data-stu-id="1fcf7-220">Create a Tableau Online test user</span></span>
<span data-ttu-id="1fcf7-221">In this section, you create a user called Britta Simon in Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-221">In this section, you create a user called Britta Simon in Tableau Online.</span></span>

1. <span data-ttu-id="1fcf7-222">On **Tableau Online**, click on **Settings** and then **Authentication** section.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-222">On **Tableau Online**, click on **Settings** and then **Authentication** section.</span></span> <span data-ttu-id="1fcf7-223">Scroll down to **Select Users** section.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-223">Scroll down to **Select Users** section.</span></span> <span data-ttu-id="1fcf7-224">Click on **Add Users** and then **Enter Email Addresses**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-224">Click on **Add Users** and then **Enter Email Addresses**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_15.png)
2. <span data-ttu-id="1fcf7-226">Select **Add users for single sign-on (SSO) authentication**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-226">Select **Add users for single sign-on (SSO) authentication**.</span></span> <span data-ttu-id="1fcf7-227">In the **Enter Email Addresses** textbox add britta.simon@contoso.com</span><span class="sxs-lookup"><span data-stu-id="1fcf7-227">In the **Enter Email Addresses** textbox add britta.simon@contoso.com</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_11.png)
3. <span data-ttu-id="1fcf7-229">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-229">Click **Create**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1fcf7-230">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="1fcf7-230">Assign the Azure AD test user</span></span>
<span data-ttu-id="1fcf7-231">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Tableau Online.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-231">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Tableau Online.</span></span>

![Assign User][200] 

<span data-ttu-id="1fcf7-233">**To assign Britta Simon to Tableau Online, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="1fcf7-233">**To assign Britta Simon to Tableau Online, perform the following steps:**</span></span>

1. <span data-ttu-id="1fcf7-234">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-234">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 
2. <span data-ttu-id="1fcf7-236">In the applications list, select **Tableau Online**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-236">In the applications list, select **Tableau Online**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_tableauonline_50.png) 
3. <span data-ttu-id="1fcf7-238">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-238">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203] 
4. <span data-ttu-id="1fcf7-240">In the All Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-240">In the All Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="1fcf7-241">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-241">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="1fcf7-243">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="1fcf7-243">Test single sign-on</span></span>
<span data-ttu-id="1fcf7-244">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-244">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="1fcf7-245">When you click the Tableau Online tile in the Access Panel, you should get automatically signed-on to your Tableau Online application.</span><span class="sxs-lookup"><span data-stu-id="1fcf7-245">When you click the Tableau Online tile in the Access Panel, you should get automatically signed-on to your Tableau Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1fcf7-246">Additional resources</span><span class="sxs-lookup"><span data-stu-id="1fcf7-246">Additional resources</span></span>
* [<span data-ttu-id="1fcf7-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1fcf7-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1fcf7-248">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1fcf7-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_general_04.png


[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_general_05.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_general_06.png
[7]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_general_050.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_general_060.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_general_070.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-tableauonline-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-tableauonline-tutorial/tutorial_general_205.png


































